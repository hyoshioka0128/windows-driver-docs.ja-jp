---
title: IRP_MJ_DEVICE_CONTROL
description: IRP\_MJ\_デバイス\_コントロール
ms.assetid: 7a7f7372-ed69-42c1-95e2-b5a593d77d22
keywords:
- IRP_MJ_DEVICE_CONTROL インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 221de9718e477bca9a5bde35cee8d23045e4ebd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550756"
---
# <a name="irpmjdevicecontrol"></a>IRP\_MJ\_デバイス\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_デバイス\_コントロール要求がや他のカーネル モード ドライバー I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。 通常この IRP は、Microsoft Win32 と呼ばれる、ユーザー モード アプリケーションに代わって送信[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数または呼び出すことがカーネル モード コンポーネントに代わって[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)します。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーは、抽出して、open のボリュームでは、ハンドルで、要求が発行されたかどうかを確認するファイル オブジェクトをデコードする必要があります。 この場合、ファイル システム ドライバーは、ボリュームがマウントされた記憶域デバイスのデバイス ドライバーを IRP を渡す必要があります。 それ以外の場合は、ドライバーは IRP を失敗する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、必要な処理を実行、フィルターの性質に応じて IRP を完了するか、またはスタック上の次の下位ドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP の[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所、デバイス制御要求の処理には、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ターゲット デバイスのデバイス ドライバーに渡されるシステム指定の入力バッファーへのポインター。 メソッドの使用\_バッファーに格納された、またはメソッド\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。 詳細については、の説明を参照して、 *IoStatusBlock*パラメーターを[ **ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)します。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
ターゲット デバイスのデバイス ドライバーに渡される出力バッファーを記述するメモリ記述子一覧 (MDL) のアドレス。 メソッドの使用\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irp--requestormode"></a>*Irp-&gt;requestormode で*  
か、操作を要求するプロセスの実行モードを示します**kernelmode である**または**UserMode**します。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ターゲット デバイスのデバイス ドライバーに渡される呼び出し元が指定の出力バッファーへのポインター。 メソッドの使用\_バッファーに格納された、またはメソッド\_どちら I/O。 このパラメーターは省略可能または必須であるかどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_デバイス\_コントロール、使用する必要があります。

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_デバイス\_コントロール。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.InputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;AssociatedIrp.SystemBuffer*します。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp-&gt;Parameters.DeviceIoControl.IoControlCode*  
ターゲット デバイスのデバイス ドライバーに渡される IOCTL 関数コードです。

IOCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565406)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters.DeviceIoControl.OutputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;UserBuffer*します。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters.DeviceIoControl.Type3InputBuffer*  
メソッドを使用するカーネル モードの要求の入力バッファーに\_NEITHER します。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IoGetFunctionCodeFromCtlCode**](https://msdn.microsoft.com/library/windows/hardware/ff549236)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**IRP\_MJ\_デバイス\_コントロール (WDK カーネル リファレンス)**](https://msdn.microsoft.com/library/windows/hardware/ff550744)

[I/O 制御コードを使用](https://msdn.microsoft.com/library/windows/hardware/ff565406)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






