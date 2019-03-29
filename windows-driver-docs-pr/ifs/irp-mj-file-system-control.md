---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP\_MJ\_ファイル\_システム\_コントロール
ms.assetid: 9df42b58-5820-44fd-8e55-0195807be951
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- IRP_MJ_FILE_SYSTEM_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 961bcb465af3150829a5e9bee1ee28b2d42ac47e
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464340"
---
# <a name="irpmjfilesystemcontrol"></a>IRP\_MJ\_ファイル\_システム\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_ファイル\_システム\_コントロール要求がや他のカーネル モード ドライバー I/O マネージャーとその他のオペレーティング システム コンポーネントによって送信されます。 送信できる、たとえば、ユーザー モード アプリケーションには、Microsoft Win32 が呼び出されたときに[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)ファイル システム I/O コントロール (FSCTL) 要求を送信する関数。

## <a name="operation-file-system-drivers"></a>操作:ファイル システム ドライバー


ファイル システム ドライバーや認識エンジンには、必要なファイル システム コントロール操作を決定するマイナー関数コードを確認する必要があります。

ファイル システム ドライバーは、次のマイナー関数コードを処理する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_KERNEL_CALL</p></td>
<td align="left"><p>この要求は、IRP_MN_USER_FS_REQUEST と同じです (次で説明されている) が、要求元が信頼されているカーネル コンポーネント。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_MOUNT_VOLUME</p></td>
<td align="left"><p>ボリュームのマウント要求を示します。 ファイル システム ドライバーは、形式と一致しません、ファイル システムのボリュームには、この IRP を受信する場合、ファイル システム ドライバーは STATUS_UNRECOGNIZED_VOLUME を返す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_USER_FS_REQUEST</p></td>
<td align="left"><p>Microsoft Win32 DeviceIoControl 関数と呼ばれる、ユーザー モード アプリケーションに代わって可能性がありますまたはカーネル モード コンポーネントと呼ばれるに代わって、FSCTL の要求を示します<a href="https://msdn.microsoft.com/library/windows/hardware/ff566441" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566441)"> <strong>ZwDeviceIoControlFile</strong></a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong></a>します。</p>
<p>FSCTL 要求の詳細については、Microsoft Windows SDK ドキュメントの「デバイスの入力と出力コントロールのコード」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_VERIFY_VOLUME</p></td>
<td align="left"><p>ボリュームの確認要求を示します。 リムーバブル メディアの場合、ファイル システムは、メディアを取り外し、ファイル システムで動作していたのと同じボリュームがまだことを確認に返されることが検出されると、ボリュームを検証しなければなりません。 ボリュームを変更した場合、ファイル システムがすべて未処理のハンドルが無効にする必要があります。 この新しいメディア上のファイル システムが変更された場合も、エラーを返しますがされます。 この要求は、フロッピー ディスク ドライブの最もよく使用されます。</p></td>
</tr>
</tbody>
</table>

 

ファイル システムの認識機能は、次のようなマイナー関数コードを処理する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IRP_MN_LOAD_FILE_SYSTEM</p></td>
<td align="left"><p>システムのファイルの読み込み要求を示します。</p></td>
</tr>
</tbody>
</table>

 

要求された操作を実行すると、ファイル システム ドライバーまたは認識エンジンが IRP を完了する必要があります。

## <a name="operation-files-system-filter-drivers"></a>操作:ファイル システム フィルター ドライバー


フィルター ドライバーは、スタックの次の下位ドライバーには、この IRP を渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイル システムまたはフィルター ドライバーは呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)ポインターを取得する、独自の特定の IRP で[**場所スタック**](https://msdn.microsoft.com/library/windows/hardware/ff550659)、IRP として次の一覧に示すように*IrpSp*します。 (IRP が示した*Irp*)。ドライバーは IRP の IRP スタックの場所、ファイル システムの制御要求の処理には、次のメンバーで設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*デバイス オブジェクト*  
ターゲット デバイスのオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp.SystemBuffer*  
ターゲット ボリュームのファイル システムまたはファイル システム フィルター ドライバーに渡されるシステム指定の入力バッファーへのポインター。 メソッドの使用\_バッファーに格納された、またはメソッド\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定のファイル システムの制御コードに依存します。

<a href="" id="irp--iostatus"></a>*Irp-&gt;IoStatus*  
ポインター、 [ **IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)最終的な完了の状態と、要求された操作に関する情報を受け取る。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
ターゲット ボリュームのファイル システムまたはファイル システム フィルター ドライバーに渡される出力バッファーを記述するメモリ記述子一覧 (MDL) のアドレス。 メソッドの使用\_ダイレクト I/O。 このパラメーターが必要かどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ターゲット ボリュームのファイル システムまたはファイル システム フィルター ドライバーに渡される呼び出し元が指定の出力バッファーへのポインター。 メソッドの使用\_バッファーに格納された、またはメソッド\_どちら I/O。 このパラメーターは省略可能または必須であるかどうかは、特定の I/O 制御コードに依存します。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
関連付けられているファイル オブジェクトへのポインター*デバイス オブジェクト*します。

*IrpSp -&gt;FileObject*パラメーターにはへのポインターが含まれています、 **RelatedFileObject**フィールドに、これは、ファイルも\_オブジェクトの構造体。 **RelatedFileObject**ファイルのフィールド\_IRP の処理中にオブジェクトの構造が有効なない\_MJ\_ファイル\_システム\_コントロール、使用する必要があります。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
IRP の次のフラグを設定する\_MN\_確認\_ボリューム。

SL\_許可\_RAW\_マウント

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP を指定します\_MJ\_ファイル\_システム\_コントロール。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかです。

-   IRP\_MN\_カーネル\_を呼び出す
-   IRP\_MN\_ロード\_ファイル\_システム
-   IRP\_MN\_マウント\_ボリューム
-   IRP\_MN\_ユーザー\_FS\_要求
-   IRP\_MN\_確認\_ボリューム

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp-&gt;Parameters.FileSystemControl.FsControlCode*  
ターゲット ボリュームのファイル システムまたはファイル システム フィルター ドライバーに渡される FSCTL 関数コードです。 IRP で使用するため\_MN\_ユーザー\_FS\_のみを要求します。

IOCTL および FSCTL 要求の詳細については、次を参照してください[I/O 制御コードを使用して](https://msdn.microsoft.com/library/windows/hardware/ff565406)で、*カーネル モードのアーキテクチャ ガイド*と"デバイスの入力と出力の制御コード"、Microsoft Windows sdk。ドキュメントです。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters.FileSystemControl.InputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;AssociatedIrp.SystemBuffer*します。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters.FileSystemControl.OutputBufferLength*  
によって示されるバッファーのバイト サイズ*Irp -&gt;UserBuffer*します。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters.FileSystemControl.Type3InputBuffer*  
メソッドを使用してカーネル モード要求を入力バッファー\_NEITHER します。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp-&gt;Parameters.MountVolume.DeviceObject*  
ボリュームがマウントされているがいる実際のデバイスのデバイス オブジェクトへのポインター。 ファイル システム フィルター ドライバーは、このパラメーターを使用する必要があります。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp-&gt;Parameters.MountVolume.Vpb*  
ボリュームがマウントされるボリューム パラメーター ブロック (VPB) へのポインター。 リムーバブル メディアをサポートするファイル システムには、このパラメーターに渡されるに使用されていた VPB を置き換えることがあります。 このようなファイル システム ボリュームがマウントされると、このポインターできますされなくと想定されますを有効にします。 次のように、これらのファイル システムをフィルター処理、ファイル システム フィルター ドライバーはこのパラメーターを使用する必要があります。IRP がドライバーの下位レベルまでを送信する前に、フィルターがの値を保存する必要があります*IrpSp -&gt;Parameters.MountVolume.Vpb -&gt;RealDevice*します。 ボリュームが正常にマウントされると、フィルターは、正しい VPB ポインターを取得するのに記憶域デバイスのオブジェクトへのポインターを使用できます。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp-&gt;Parameters.VerifyVolume.DeviceObject*  
検証するボリュームのデバイス オブジェクトへのポインター。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp-&gt;Parameters.VerifyVolume.Vpb*  
検証するボリュームの VPB へのポインター。

## <a name="see-also"></a>関連項目


[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IO\_状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff550671)

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)

[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)

[**IoGetCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549174)

[**IRP**](https://msdn.microsoft.com/library/windows/hardware/ff550694)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






