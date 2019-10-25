---
title: カーネルモードドライバーによる HID レポートの送信
description: カーネルモードドライバーによる HID レポートの送信
ms.assetid: ff3d090f-cf76-40a7-9215-8440a592f303
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 266de90bb6b6505649c4a0c698492c5d023f60f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841558"
---
# <a name="sending-hid-reports-by-kernel-mode-drivers"></a>カーネルモードドライバーによる HID レポートの送信


カーネルモードドライバーでは、出力レポートを HID コレクションに継続的に送信するための主なアプローチとして、 [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求を使用する必要があります。 また、ドライバーは IOCTL\_HID\_使用して\_*Xxx*要求を設定し、出力レポートと機能レポートをコレクションに送信することもできます。 ただし、ドライバーは、これらの i/o 要求のみを使用して、コレクションの現在の状態を設定する必要があります。 一部のデバイスでは、 [**IOCTL\_HID\_設定\_出力\_レポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report)がサポートされていないため、この要求が使用された場合は応答しなくなります。

詳細については、「 [IRP\_MJ を使用した\_書き込み要求](#using-irp-mj-write-requests)」と「 [IOCTL\_HID\_SET\_Xxx Requests](#using-ioctl-hid-set-xxx-requests)」を参照してください。

### <a href="" id="using-irp-mj-write-requests"></a>IRP\_MJ\_書き込み要求の使用

WDM 以外の Windows 2000 ドライバー、および Windows XP 以降のバージョンのドライバーでは、コレクションに送信されるすべての書き込み要求に対して単一の IRP を使用できます。 ただし、Windows 2000 WDM ドライバーは、書き込み要求ごとに新しい IRP を割り当てる必要があります。 Irp の使用方法と再利用方法の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)と[irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)の再利用」を参照してください。

ドライバーが書き込み IRP を再利用する場合、IRP の[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンは、状態が [状態] である要求を完了する必要があります (これにより、irp は解放されません)。\_処理\_必要が\_ます。 ドライバーが IRP を必要としなくなった場合、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)と[**Iofreeirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)を呼び出して irp を完了し、解放する必要があります。 たとえば、ドライバーは通常、[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンで IRP を完了して解放します。また、デバイスが削除された後に解放することもできます。

ドライバーが1つの書き込み要求に対してのみ IRP を使用する場合、IRP の[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが完了し、irp が解放され、状態\_SUCCESS が返されます。

出力レポートを送信する前に、ドライバーはまず、「 [HID レポートの初期化](initializing-hid-reports.md)」で説明されているように、出力レポートバッファーを初期化して設定する必要があります。 ドライバーは、その後、MDL を使用して、書き込み要求の出力レポートバッファーをマップする必要があります。 ドライバーは[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)を呼び出して、出力レポート用に mdl を割り当て、出力レポートバッファーの mdl アドレスに書き込み Irp の**Irp&gt;mdladdress**メンバーを設定します。 ドライバーが不要になった場合は、レポートバッファーと MDL を解放する必要があります。

書き込み IRP の MDL アドレスを設定するだけでなく、ドライバーは次の下位レベルのドライバーの i/o スタックの場所も設定する必要があります。 ドライバーは、 [**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出すことによって、次の下位レベルのドライバーの i/o スタックの場所へのアクセスを取得します。 このドライバーは、i/o スタックの場所の次のメンバーを設定します。

<a href="" id="parameters-write-length"></a>**Parameters. Write. Length**  
出力レポートの長さをバイト単位で設定します。 これは、コレクションの[**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体の**OutputReportByteLength**メンバーによって指定された、HID コレクションの出力レポートの長さに設定する必要があります。

<a href="" id="parameters-write-key"></a>**Parameters. Write. Key**  
を0に設定します。

<a href="" id="parameters-write-byteoffset-quadpart"></a>**Parameters. ByteOffset. QuadPart**  
を0に設定します。

<a href="" id="majorfunction"></a>**MajorFunction**  
IRP\_MJ\_WRITE に設定します。

<a href="" id="fileobject"></a>**ファ**  
は、HID コレクションで開いているファイルを表すファイルオブジェクトポインターに設定されます。

### <a href="" id="using-ioctl-hid-set-xxx-requests"></a>IOCTL\_HID\_使用して\_Xxx 要求を設定する

ドライバーは、次の i/o 要求を使用して、出力と機能のレポートを HID コレクションに送信することもできます。

<a href="" id="ioctl-hid-set-output-report"></a>[**IOCTL\_HID\_SET\_出力\_レポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_output_report)  
出力レポートをコレクションに送信します (Windows XP 以降のバージョン)。

<a href="" id="ioctl-hid-set-feature"></a>[**IOCTL\_HID\_SET\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_set_feature)  
機能レポートをコレクションに送信します。

 

 




