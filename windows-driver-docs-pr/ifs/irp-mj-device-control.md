---
title: IRP_MJ_DEVICE_CONTROL
description: IRP\_MJ\_DEVICE\_CONTROL
ms.assetid: 7a7f7372-ed69-42c1-95e2-b5a593d77d22
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_DEVICE_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f6d9682a343737cb3d2fb0a90cf11be066afb3
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977685"
---
# <a name="irp_mj_device_control"></a>IRP\_MJ\_DEVICE\_CONTROL


## <a name="when-sent"></a>送信時


IRP\_MJ\_デバイス\_制御要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 通常、この IRP は、Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出したユーザーモードアプリケーションの代わりに、または[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)を呼び出したカーネルモードコンポーネントの代わりに送信されます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ボリュームを開いているハンドルで要求が発行されているかどうかを判断するために、ファイルオブジェクトを抽出してデコードする必要があります。 この場合は、ファイルシステムドライバーが IRP を、ボリュームがマウントされている記憶装置のデバイスドライバーに渡す必要があります。 それ以外の場合、ドライバーは IRP を失敗させる必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは必要な処理を実行する必要があります。フィルターの性質によっては、IRP を完了するか、スタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP に対して[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタック位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧に*irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、デバイス制御要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
ターゲットデバイスのデバイスドライバーに渡されるシステム指定の入力バッファーへのポインター。 バッファーまたはメソッド\_直接 i/o に\_ために使用されます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。 詳細については、 [**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)の*iostatusblock*パラメーターの説明を参照してください。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
ターゲットデバイスのデバイスドライバーに渡される出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッド\_直接 i/o に使用されます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--requestormode"></a>*Irp-&gt;Irp->requestormode*  
操作を要求したプロセスの実行モード ( **kernelmode で**または**モード**) を示します。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ターゲットデバイスのデバイスドライバーに渡される、呼び出し元から提供される出力バッファーへのポインター。 I/o ではない\_バッファーまたはメソッド\_に使用されます。 このパラメーターが省略可能か必須かは、特定の i/o 制御コードによって決まります。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_デバイス\_制御の処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であるため、使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_デバイス\_コントロールを指定します。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters. DeviceIoControl. InputBufferLength*  
*Irp&gt;AssociatedIrp*によってポイントされるバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp-&gt;Parameters. DeviceIoControl. IoControlCode*  
ターゲットデバイスのデバイスドライバーに渡される IOCTL 関数コード。

IOCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters. DeviceIoControl. OutputBufferLength*  
*Irp&gt;UserBuffer*が指すバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters. DeviceIoControl. Type3InputBuffer*  
メソッドを使用するカーネルモード要求の入力バッファー\_ません。

## <a name="see-also"></a>「


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IoGetFunctionCodeFromCtlCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetfunctioncodefromctlcode)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP\_MJ\_デバイス\_コントロール (WDK カーネルリファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

[I/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






