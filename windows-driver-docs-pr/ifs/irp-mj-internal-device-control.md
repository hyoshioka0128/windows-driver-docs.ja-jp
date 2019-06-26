---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL
ms.assetid: a60325d5-993f-4505-bded-2c2be9782492
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_INTERNAL_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e941da922eb457c295de063c4034e04bd0291f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384826"
---
# <a name="irpmjinternaldevicecontrol"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


## <a name="when-sent"></a>送信時


IRP\_MJ\_内部\_デバイス\_コントロール要求がや他のカーネル モード ドライバー I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。

異なり[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)要求、IRP\_MJ\_内部\_デバイス\_コントロールの要求は、カーネル モードのコンポーネント間の通信にのみ使用されます。 IRP を while\_MJ\_デバイス\_制御要求への呼び出しに通常発生元**DeviceIoControl**または[ **ZwDeviceIoControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566441)、これらのルーチンは IRP を作成できません\_MJ\_内部\_デバイス\_に対する制御要求。 IRP の両方の種類を作成して呼び出すことによって、 [ **IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、ボリューム オープンを表すハンドルで、要求が発行されたかどうかを確認するファイル オブジェクトをデコードする必要があります。 この場合、ファイル システム ドライバーは、ボリュームがマウントされた記憶域デバイスのデバイス ドライバーを IRP を渡す必要があります。 それ以外の場合は、ドライバーは IRP を失敗する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、必要な処理を実行、フィルターの性質に応じて IRP を完了するか、またはスタック上の次の下位ドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所、デバイス制御要求の処理には、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ターゲット デバイスのデバイス ドライバーに渡されるシステム指定の入力バッファーへのポインター。 メソッドの使用\_バッファーに格納された、またはメソッド\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)最終的な完了の状態と、要求された操作に関する情報を受け取る。 詳細については、の説明を参照して、 *IoStatusBlock*パラメーターを[ **ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)します。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
ターゲット デバイスのデバイス ドライバーに渡される出力バッファーを記述したメモリ記述子一覧 (MDL) のアドレス。 メソッドの使用\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irp--requestormode"></a>*Irp-&gt;requestormode で*  
か、操作を要求するプロセスの実行モードを示します**kernelmode である**または**UserMode**します。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ターゲット デバイスのデバイス ドライバーに渡される呼び出し元が指定の出力バッファーへのポインター。 このパラメーターは、メソッドの使用は\_バッファーに格納された、またはメソッド\_も I/O。 このパラメーターは省略可能または必須であるかどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_内部\_デバイス\_コントロールとすることはできませんこのオプションを使用するとします。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_内部\_デバイス\_コントロール。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.InputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;AssociatedIrp.SystemBuffer*します。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp-&gt;Parameters.DeviceIoControl.IoControlCode*  
ターゲット デバイスのデバイス ドライバーに渡される IOCTL 関数コードです。

IOCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.OutputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;UserBuffer*します。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters.DeviceIoControl.Type3InputBuffer*  
メソッドを使用してカーネル モード要求を入力バッファー\_NEITHER します。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IoGetFunctionCodeFromCtlCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetfunctioncodefromctlcode)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール (WDK カーネル リファレンス)** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

[I/O 制御コードを使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






