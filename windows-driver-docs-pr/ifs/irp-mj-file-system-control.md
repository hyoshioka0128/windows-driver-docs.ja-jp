---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP\_MJ\_ファイル\_システム\_コントロール
ms.assetid: 9df42b58-5820-44fd-8e55-0195807be951
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_FILE_SYSTEM_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_FILE_SYSTEM_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25545db49d9ca3f3bd6a0721473c2c75cd14cfd
ms.sourcegitcommit: c9fc8f401d13ea662709ad1f0cb41c810e7cb4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2020
ms.locfileid: "76977681"
---
# <a name="irp_mj_file_system_control"></a>IRP\_MJ\_ファイル\_システム\_コントロール


## <a name="when-sent"></a>送信時


IRP\_MJ\_FILE\_SYSTEM\_CONTROL 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出してファイルシステム i/o 制御 (FSCTL) 要求を送信した場合などに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー


ファイルシステムドライバーまたはレコグナイザーは、マイナー関数のコードを確認して、どのファイルシステム制御操作が要求されているかを判断する必要があります。

ファイルシステムドライバーは、次のマイナー関数コードを処理する必要があります。

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
<td align="left"><p>この要求は IRP_MN_USER_FS_REQUEST (次に説明) と同じですが、要求のソースは信頼されたカーネルコンポーネントである点が異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_MOUNT_VOLUME</p></td>
<td align="left"><p>ボリュームマウント要求を示します。 ファイルシステムドライバーがファイルシステムの形式と一致しないボリュームに対してこの IRP を受信した場合、ファイルシステムドライバーは STATUS_UNRECOGNIZED_VOLUME を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IRP_MN_USER_FS_REQUEST</p></td>
<td align="left"><p>FSCTL 要求を示します。これは、Microsoft Win32 DeviceIoControl 関数を呼び出したユーザーモードアプリケーションに代わって、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff566441" data-raw-source="[&lt;strong&gt;ZwDeviceIoControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566441)"><strong>ZwDeviceIoControlFile</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>を呼び出したカーネルモードコンポーネントの代理として発生する可能性があります。</p>
<p>FSCTL 要求の詳細については、Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IRP_MN_VERIFY_VOLUME</p></td>
<td align="left"><p>ボリューム検証要求を示します。 リムーバブルメディアの場合、ファイルシステムは、メディアが削除され、ファイルシステムが以前に使用していたボリュームと同じボリュームであることを検出したときに、そのボリュームを確認する必要があります。 ボリュームが変更されている場合、ファイルシステムは未処理のハンドルをすべて無効にする必要があります。 また、この新しいメディアのファイルシステムが変更された場合にもエラーが返されます。 この要求は、ほとんどの場合、フロッピードライブに使用されます。</p></td>
</tr>
</tbody>
</table>

 

ファイルシステムのレコグナイザーは、次のマイナー関数コードを処理する必要があります。

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
<td align="left"><p>ファイルシステム要求の読み込みを示します。</p></td>
</tr>
</tbody>
</table>

 

要求された操作を実行した後、ファイルシステムドライバーまたはレコグナイザーが IRP を完了する必要があります。

## <a name="operation-files-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー


フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター


ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、ファイルシステムコントロール要求の処理中に、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

<a href="" id="deviceobject"></a>*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp-&gt;AssociatedIrp*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡されるシステム指定の入力バッファーへのポインター。 バッファーまたはメソッド\_直接 i/o に\_ために使用されます。 このパラメーターが必須かどうかは、特定のファイルシステム制御コードによって異なります。

<a href="" id="irp--iostatus"></a>*Irp&gt;IoStatus*  
最終的な完了状態と要求された操作に関する情報を受け取る、 [**IO\_ステータス\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造へのポインター。

<a href="" id="irp--mdladdress"></a>*Irp-&gt;MdlAddress*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッド\_直接 i/o に使用されます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--userbuffer"></a>*Irp-&gt;UserBuffer*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される、呼び出し元から提供される出力バッファーへのポインター。 I/o ではない\_バッファーまたはメソッド\_に使用されます。 このパラメーターが省略可能か必須かは、特定の i/o 制御コードによって決まります。

<a href="" id="irpsp--fileobject"></a>*IrpSp-&gt;FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp-&gt;FileObject*パラメーターには、関連する**fileobject**フィールドへのポインターが含まれています。これは、ファイル\_オブジェクト構造体でもあります。 IRP\_MJ\_ファイル\_システム\_コントロールの処理中は、ファイル\_オブジェクト構造の関連性の**あるフィールドは**無効であるため、使用できません。

<a href="" id="irpsp--flags"></a>*IrpSp-&gt;フラグ*  
次のフラグは、IRP\_に対して設定できます。\_ボリューム\_確認してください。

SL\_\_RAW\_マウントが許可

<a href="" id="irpsp--majorfunction"></a>*IrpSp-&gt;MajorFunction*  
IRP\_MJ\_ファイル\_システム\_コントロールを指定します。

<a href="" id="irpsp--minorfunction"></a>*IrpSp-&gt;MinorFunction*  
次のいずれかです。

-   IRP\_\_カーネル\_呼び出し
-   IRP\_\_ファイル\_システム\_読み込み
-   IRP\_\_マウント\_ボリューム
-   IRP\_\_ユーザー\_FS\_要求
-   IRP\_\_確認\_ボリューム

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp-&gt;Parameters. FileSystemControl. FsControlCode*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される FSCTL 関数コード。 IRP\_で使用する場合は\_ユーザー\_FS\_要求のみです。

IOCTL 要求と FSCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp-&gt;Parameters. Filesystembufferlength*  
*Irp&gt;AssociatedIrp*によってポイントされるバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp-&gt;Parameters. Filesystembufferlength*  
*Irp&gt;UserBuffer*が指すバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp-&gt;Parameters. FileSystemControl. Type3InputBuffer*  
メソッドを使用したカーネルモード要求の入力バッファー\_ません。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp-&gt;Parameters. MountVolume. DeviceObject*  
ボリュームがマウントされる実際のデバイスのデバイスオブジェクトへのポインター。 ファイルシステムフィルタードライバーでは、このパラメーターを使用しないでください。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp-&gt;Parameters. MountVolume. Vpb*  
マウントするボリュームのボリュームパラメーターブロック (VPB) へのポインター。 リムーバブルメディアをサポートするファイルシステムでは、このパラメーターで渡された VPB を以前に使用した VPB に置き換えることができます。 このようなファイルシステムでは、ボリュームがマウントされた後、このポインターが有効であるとは見なされなくなります。 これらのファイルシステムをフィルター処理するファイルシステムフィルタードライバーでは、次のように、このパラメーターを使用する必要があります。 IRP を下位レベルのドライバーに送信する前に、フィルターにより*Irpsp-&gt;MountVolume-&gt;RealDevice*の値が保存されます。 ボリュームが正常にマウントされると、フィルターはこのポインターを使用して、正しい VPB ポインターを取得できます。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp-&gt;Parameters. VerifyVolume. DeviceObject*  
検証するボリュームのデバイスオブジェクトへのポインター。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp-&gt;パラメーター。 VerifyVolume. Vpb*  
検証するボリュームの VPB へのポインター。

## <a name="see-also"></a>「


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






