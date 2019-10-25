---
title: カーネルモードドライバーによる HID レポートの取得
description: このトピックでは、HID 入力レポートを継続的に取得するための主なアプローチとして、カーネルモードドライバーで IRP_MJ_READ 要求を使用する方法について説明します。
ms.assetid: 017481f1-8021-4fd5-ab8e-f09f6006e616
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ec133e6e0b0e67653339ae64e3e612f60e20f6d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841568"
---
# <a name="obtaining-hid-reports-by-kernel-mode-drivers"></a>カーネルモードドライバーによる HID レポートの取得


このトピックでは、HID 入力レポートを継続的に取得するための主なアプローチとして、カーネルモードドライバーで[**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求を使用する方法について説明します。

連続する読み取り要求は、コレクションから受け取った順序で入力レポートを返します。 また、ドライバーは IOCTL\_HID\_使用して\_*Xxx*要求を取得し、入力と機能のレポートを取得することもできます。 ただし、ドライバーは、デバイスの現在の状態を取得するために、これらの i/o 要求のみを使用する必要があります。 ドライバーが IOCTL\_\_\_\_を使用して入力レポートを継続的に取得しようとすると、レポートが失われる可能性があります。 また、一部のデバイスでは、IOCTL\_HID\_GET\_入力\_レポートがサポートされていないため、この要求が使用された場合は応答しなくなります。

以下のセクションで詳細を説明します。

### <a href="" id="using-irp-ml-read-requests"></a>IRP\_MJ\_読み取り要求の使用

WDM 以外の Windows 2000 ドライバー、および Windows XP 以降のバージョンのドライバーでは、デバイスに対するすべての読み取り要求に対して単一の IRP を使用できます。 ただし、Windows 2000 WDM ドライバーは、読み取り要求ごとに新しい IRP を割り当てる必要があります。 Irp の使用方法と再利用方法に関する一般的な情報については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)と[irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)の再利用」を参照してください。

ドライバーが IRP を再利用する場合、IRP の[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、状態が [状態] である要求を完了する必要があります (これにより、irp は解放されません)。\_の処理\_必要があり\_。 ドライバーが IRP を必要としなくなった場合、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)と[**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出して irp を完了し、解放する必要があります。 たとえば、ドライバーは通常、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンで IRP を完了して解放します。また、デバイスが削除された後に解放することもできます。

ドライバーが1つの読み取り要求に対してのみ IRP を使用する場合は、IRP の**Iocompletion**ルーチンが完了し、irp が解放され、状態\_SUCCESS が返されます。

ドライバーが入力レポートを要求できるようにするには、まず、非ページメモリプールからゼロで初期化された入力レポートバッファーを割り当てる必要があります。 バッファーのサイズ (バイト単位) は、HID コレクションの[**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体の**InputReportByteLength**メンバーによって指定されます。 次に、ドライバーは、MDL を使用して、読み取り要求の入力レポートバッファーをマップする必要があります。 ドライバーは[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を呼び出して、入力レポートバッファーの mdl を割り当て、読み取り Irp の**Irp&gt;mdladdress**メンバーを入力レポートバッファーの mdl アドレスに設定します。 ドライバーは、不要になったときに、レポートバッファーと MDL を解放する必要があります。

読み取り IRP の MDL アドレスを設定するだけでなく、ドライバーは次の下位レベルのドライバーの i/o スタックの場所も設定する必要があります。 ドライバーは、 [**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出すことによって、次の下位レベルのドライバーの i/o スタックの場所へのアクセスを取得します。 このドライバーは、i/o スタックの場所の次のメンバーを設定します。

<a href="" id="parameters-read-length"></a>**Parameters、Read. Length**  
読み取りバッファーのサイズ (バイト単位) に設定します。 これは、HID コレクションの[**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体の**InputReportByteLength**メンバーによって指定された値以上である必要があります。

<a href="" id="parameters-read-key"></a>**パラメーター。読み取ります。キー**  
を0に設定します。

<a href="" id="parameters-read-byteoffset-quadpart"></a>**Parameters. ByteOffset. QuadPart**  
を0に設定します。

<a href="" id="majorfunction"></a>**MajorFunction**  
IRP\_MJ\_READ に設定します。

<a href="" id="fileobject"></a>**ファ**  
は、HID コレクションで開いているファイルを表すファイルオブジェクトポインターに設定されます。

ドライバーは、入力レポートを取得した後、「 [HID レポートの解釈](interpreting-hid-reports.md)」で説明されているように、コントロールデータにアクセスできます。

### <a href="" id="using-ioctl-hid-get-xxx-requests"></a>IOCTL\_HID\_使用して\_Xxx 要求を取得する

ドライバーは、次の i/o 要求を使用して、HID コレクションから最新の入力と機能のレポートを取得できます。

<a href="" id="ioctl-hid-get-input-report"></a>[**IOCTL\_HID\_\_入力\_レポートを取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_input_report)  
HID コレクションから入力レポートを返します (Windows XP 以降のバージョン)。

<a href="" id="ioctl-hid-get-feature"></a>[**IOCTL\_HID\_\_機能の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_feature)  
HID コレクションから機能レポートを返します。

ドライバーは、特定のレポートの返却を要求できます。 これらの i/o 要求を使用して特定のレポートを取得するために、ドライバーはまず出力レポートバッファーを割り当て、次にバッファーの最初のバイトを特定のレポート ID に設定します。 詳細については、「 [HID レポートの解釈](interpreting-hid-reports.md)」を参照してください。

 

 




