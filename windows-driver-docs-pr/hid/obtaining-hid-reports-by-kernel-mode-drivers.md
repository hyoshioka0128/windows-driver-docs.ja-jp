---
title: カーネル モード ドライバーでの HID レポートを取得します。
description: このトピックで使用方法について説明、カーネル モード ドライバーが IRP_MJ_READ 要求の主なアプローチとして HID 入力レポートを継続的に取得するため。
ms.assetid: 017481f1-8021-4fd5-ab8e-f09f6006e616
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f8d7746827d9ea3bb369419e178e8aac1aacefa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375892"
---
# <a name="obtaining-hid-reports-by-kernel-mode-drivers"></a>カーネル モード ドライバーでの HID レポートを取得します。


このトピックでは、カーネル モード ドライバーの使用方法について説明します[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)の主なアプローチとして HID を継続的に取得するレポートの入力を要求します。

連続した読み取り要求は、コレクションから受信した順序で入力のレポートを返します。 ドライバーは、IOCTL を使用できますも\_HID\_取得\_*Xxx*入力と機能のレポートを取得する要求。 ただし、ドライバーは、デバイスの現在の状態を取得するのにこれらの I/O 要求を使用する必要がありますのみ。 場合は、ドライバーは、IOCTL の使用を試みます\_HID\_取得\_入力\_入力のレポートを継続的に取得するレポート、レポートが失われることができます。 さらに、一部のデバイスがサポートしていません IOCTL\_HID\_取得\_入力\_レポートがこの要求を使用する場合に応答しなくなるとします。

次のセクションでは、詳細を提供します。

### <a href="" id="using-irp-ml-read-requests"></a>IRP を使用して\_MJ\_読み取り要求

Windows 2000 の非 WDM ドライバー、および Windows XP およびそれ以降のバージョンのドライバーは、デバイスへのすべての読み取り要求の 1 つの IRP を使用できます。 ただし、Windows 2000 WDM ドライバーでは、読み取り要求ごとに新しい IRP を割り当てる必要があります。 使用して、Irp を再利用する方法についての概要については、次を参照してください。 [Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)と[Irp の再利用](https://docs.microsoft.com/windows-hardware/drivers/kernel/reusing-irps)します。

ドライバーが IRP、IRP の再利用かどうか[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンは、状態の状態で要求を完了する必要があります\_詳細\_処理\_必須 (および notIRP を解放)。 ドライバーは IRP が不要になった必要がある場合、完了して IRP を呼び出すことによって解放[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)と[ **IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)します。 たとえば、ドライバー可能性があります通常完了し、解放で IRP その[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチン、以降のデバイスを削除します。

1 つだけ要求を読み取り、IRP のドライバーが IRP を使用している場合**IoCompletion**完了し、IRP を無料し、状態を返す必要がありますルーチン\_成功します。

ドライバーは、入力のレポートを要求できます、前に最初に割り当てる必要があります非ページ メモリ プールからの入力のレポートをゼロに初期化バッファー。 バッファーのバイト単位で、サイズが指定された、 **InputReportByteLength** HID コレクションのメンバー [ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)構造体。 ドライバーは、読み取り要求のレポートの入力バッファーをマップするのに、MDL を使用する必要があります。 ドライバー呼び出し[ **IoAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl) MDL をレポートの入力バッファーを割り当てられません読み取り IRP の設定と**Irp -&gt;MdlAddress** MDL アドレスへのメンバーレポートの入力バッファー。 ドライバーでは、必要でなくなったときに、レポート バッファーと MDL を解放する必要があります。

読み取り設定だけでなく IRP の MDL アドレスでは、ドライバーは、[次へ] の下位レベルのドライバーの I/O スタックの場所を設定する必要がありますもします。 ドライバーを呼び出すことによって、[次へ] の下位レベルのドライバーの I/O スタックの場所へのアクセスを取得する[ **IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)します。 ドライバーは、I/O スタックの場所の次のメンバーを設定します。

<a href="" id="parameters-read-length"></a>**Parameters.Read.Length**  
読み取りバッファーのバイト単位のサイズに設定します。 によって指定された値以上にあるこの必要があります、 **InputReportByteLength** HID コレクションのメンバー [ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)構造体。

<a href="" id="parameters-read-key"></a>**Parameters.Read.Key**  
0 に設定します。

<a href="" id="parameters-read-byteoffset-quadpart"></a>**Parameters.Read.ByteOffset.QuadPart**  
0 に設定します。

<a href="" id="majorfunction"></a>**MajorFunction**  
IRP に設定\_MJ\_を読み取る。

<a href="" id="fileobject"></a>**FileObject**  
HID コレクションで、開いているファイルを表すファイル オブジェクト ポインターに設定します。

ドライバーには、入力のレポートは取得した後で説明されているようにコントロールのデータにアクセスできる[HID レポートの解釈](interpreting-hid-reports.md)します。

### <a href="" id="using-ioctl-hid-get-xxx-requests"></a>IOCTL を使用して\_HID\_取得\_Xxx 要求

ドライバーは、次の I/O 要求を使用して、HID コレクションから現在のほとんどの入力と機能のレポートを取得できます。

<a href="" id="ioctl-hid-get-input-report"></a>[**IOCTL\_HID\_取得\_入力\_レポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_input_report)  
(Windows XP およびそれ以降のバージョン) は、HID コレクションから入力のレポートを返します。

<a href="" id="ioctl-hid-get-feature"></a>[**IOCTL\_HID\_取得\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_feature)  
HID コレクションから機能のレポートを返します。

ドライバーは、特定のレポートの戻り値を要求できます。 これらの I/O 要求を使用して特定のレポートを取得するには、ドライバー最初出力レポート バッファーを割り当てたバッファーを 0 に初期化し、特定のレポート ID に、バッファー内の最初のバイトの設定 詳細については、次を参照してください。 [HID レポートの解釈](interpreting-hid-reports.md)します。

 

 




