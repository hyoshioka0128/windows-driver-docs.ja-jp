---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL (IFS)
description: IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL
ms.assetid: a60325d5-993f-4505-bded-2c2be9782492
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_INTERNAL_DEVICE_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_INTERNAL_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abbf73f934e499392c18cc2669e04a334bc31d44
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141264"
---
# <a name="irp_mj_internal_device_control-ifs"></a>IRP \_ MJ \_ 内部 \_ デバイス \_ コントロール (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ 内部 \_ デバイス \_ 制御要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。

[**Irp \_ MJ \_ デバイス \_ コントロール**](irp-mj-device-control.md)要求とは異なり、irp \_ MJ \_ 内部 \_ デバイス \_ 制御要求は、カーネルモードコンポーネント間の通信にのみ使用されます。 \_通常、irp MJ \_ デバイス \_ 制御要求は**DeviceIoControl**または[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)の呼び出しで発生しますが、これらのルーチンは、irp \_ MJ \_ 内部 \_ デバイス \_ 制御要求を作成することはできません。 ただし、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出すことによって、両方の種類の IRP を作成できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーは、ファイルオブジェクトを抽出してデコードし、開いているボリュームを表すハンドルで要求が発行されているかどうかを確認する必要があります。 この場合は、ファイルシステムドライバーが IRP を、ボリュームがマウントされている記憶装置のデバイスドライバーに渡す必要があります。 それ以外の場合、ドライバーは IRP を失敗させる必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは必要な処理を実行する必要があります。フィルターの性質によっては、IRP を完了するか、スタック上の次の下位のドライバーに渡します。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、デバイス制御要求を処理するときに、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp &gt;AssociatedIrp.SystemBuffer*  
ターゲットデバイスのデバイスドライバーに渡されるシステム指定の入力バッファーへのポインター。 メソッドのバッファーまたはメソッドの直接 i/o に使用され \_ \_ ます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。 詳細については、 [**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)の*iostatusblock*パラメーターの説明を参照してください。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; mdladdress*  
ターゲットデバイスのデバイスドライバーに渡される出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッドダイレクト i/o に使用され \_ ます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--requestormode"></a>*Irp- &gt; irp->requestormode*  
操作を要求したプロセスの実行モード ( **kernelmode で**または**モード**) を示します。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
ターゲットデバイスのデバイスドライバーに渡される、呼び出し元から提供される出力バッファーへのポインター。 このパラメーターは、メソッドの \_ バッファーまたはメソッドが i/o ではない場合に使用され \_ ます。 このパラメーターが省略可能か必須かは、特定の i/o 制御コードによって決まります。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の MJ **fileobject**フィールド \_ は、IRP 内部デバイスコントロールの処理中は無効であり、 \_ \_ \_ \_ 使用しないでください。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ \_ 内部デバイスコントロールを指定し \_ \_ ます。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp- &gt; DeviceIoControl. InputBufferLength*  
*Irp &gt;AssociatedIrp.Systembuffer*が指すバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp- &gt; DeviceIoControl。 IoControlCode*  
ターゲットデバイスのデバイスドライバーに渡される IOCTL 関数コード。

IOCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp- &gt; DeviceIoControl の長さ*  
* &gt; UserBuffer*によってポイントされるバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp- &gt; DeviceIoControl. Type3InputBuffer*  
メソッドを使用したカーネルモード要求の入力バッファーが \_ ありません。

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IoGetFunctionCodeFromCtlCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetfunctioncodefromctlcode)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ デバイス \_ コントロール**](irp-mj-device-control.md)

[**IRP \_ MJ \_ 内部 \_ デバイス \_ コントロール (WDK カーネルリファレンス)**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

[I/O 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






