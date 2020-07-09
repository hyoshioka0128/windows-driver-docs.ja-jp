---
title: IRP_MJ_FILE_SYSTEM_CONTROL (IFS)
description: IRP \_ MJ \_ ファイル \_ システム \_ コントロール
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
ms.openlocfilehash: b7ad389bacb472b51e95e3ba48504ad932d5a3e4
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141217"
---
# <a name="irp_mj_file_system_control-ifs"></a>IRP \_ MJ \_ FILE \_ SYSTEM \_ CONTROL (IFS)


## <a name="when-sent"></a>送信時


IRP \_ MJ \_ FILE \_ system \_ CONTROL 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出してファイルシステム i/o 制御 (FSCTL) 要求を送信した場合などに送信できます。

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

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp &gt;AssociatedIrp.SystemBuffer*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡されるシステム指定の入力バッファーへのポインター。 メソッドのバッファーまたはメソッドの直接 i/o に使用され \_ \_ ます。 このパラメーターが必須かどうかは、特定のファイルシステム制御コードによって異なります。

<a href="" id="irp--iostatus"></a>*Irp- &gt; iostatus*  
最後の完了状態と要求された操作に関する情報を受け取る[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; mdladdress*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される出力バッファーを記述するメモリ記述子リスト (MDL) のアドレス。 メソッドダイレクト i/o に使用され \_ ます。 このパラメーターが必須かどうかは、特定の i/o 制御コードによって異なります。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される、呼び出し元から提供される出力バッファーへのポインター。 メソッドのバッファーに使用されるか、または i/o ではないメソッドに使用され \_ \_ ます。 このパラメーターが省略可能か必須かは、特定の i/o 制御コードによって決まります。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp- &gt; FileObject*パラメーターには、関連する**FileObject**フィールドへのポインターが含まれています。これは、ファイルオブジェクト構造でも \_ あります。 ファイルオブジェクト構造の関連性のある**fileobject**フィールド \_ は、IRP MJ FILE SYSTEM CONTROL の処理中は無効である \_ ため、 \_ \_ \_ 使用しないでください。

<a href="" id="irpsp--flags"></a>*IrpSp- &gt; フラグ*  
次のフラグは、IRP を確認するボリュームに設定でき \_ \_ \_ ます。

SL に \_ よる \_ RAW \_ マウント

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
IRP \_ MJ \_ ファイルシステムコントロールを指定し \_ \_ ます。

<a href="" id="irpsp--minorfunction"></a>*IrpSp- &gt; minorfunction*  
次のいずれか:

-   IRP の全 \_ \_ カーネル \_ 呼び出し
-   IRP の全 \_ \_ 負荷の \_ ファイル \_ システム
-   IRP の全 \_ \_ マウント \_ ボリューム
-   IRP の全 \_ \_ ユーザーのユーザー \_ FS \_ 要求
-   IRP の全 \_ \_ 検査の \_ ボリューム

<a href="" id="irpsp--parameters-filesystemcontrol-fscontrolcode"></a>*IrpSp- &gt; Parameters. FileSystemControl. FsControlCode*  
ターゲットボリュームのファイルシステムまたはファイルシステムフィルタードライバーに渡される FSCTL 関数コード。 IRP の \_ \_ ユーザー \_ FS \_ 要求のみで使用します。

IOCTL 要求と FSCTL 要求の詳細については、「*カーネルモードアーキテクチャガイド*」の「 [i/o 制御コードの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)」および Microsoft Windows SDK のドキュメントの「デバイスの入力と出力の制御コード」を参照してください。

<a href="" id="irpsp--parameters-filesystemcontrol-inputbufferlength"></a>*IrpSp- &gt; Parameters. FileSystemControl. InputBufferLength*  
*Irp &gt;AssociatedIrp.Systembuffer*が指すバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-filesystemcontrol-outputbufferlength"></a>*IrpSp- &gt; Parameters. Filesystembufferlength*  
* &gt; UserBuffer*によってポイントされるバッファーのサイズ (バイト単位)。

<a href="" id="irpsp--parameters-filesystemcontrol-type3inputbuffer"></a>*IrpSp- &gt; Parameters Type3InputBuffer*  
メソッドを使用したカーネルモード要求の入力バッファーが \_ ありません。

<a href="" id="irpsp--parameters-mountvolume-deviceobject"></a>*IrpSp- &gt; MountVolume. DeviceObject*  
ボリュームがマウントされる実際のデバイスのデバイスオブジェクトへのポインター。 ファイルシステムフィルタードライバーでは、このパラメーターを使用しないでください。

<a href="" id="irpsp--parameters-mountvolume-vpb"></a>*IrpSp- &gt; MountVolume. Vpb*  
マウントするボリュームのボリュームパラメーターブロック (VPB) へのポインター。 リムーバブルメディアをサポートするファイルシステムでは、このパラメーターで渡された VPB を以前に使用した VPB に置き換えることができます。 このようなファイルシステムでは、ボリュームがマウントされた後、このポインターが有効であるとは見なされなくなります。 これらのファイルシステムをフィルター処理するファイルシステムフィルタードライバーでは、次のように、このパラメーターを使用する必要があります。 IRP を下位レベルのドライバーに送信する前に、フィルターによって MountVolume の値が保存されます。 * &gt; &gt; * ボリュームが正常にマウントされると、フィルターはこのポインターを使用して、正しい VPB ポインターを取得できます。

<a href="" id="irpsp--parameters-verifyvolume-deviceobject"></a>*IrpSp- &gt; Parameters. VerifyVolume. DeviceObject*  
検証するボリュームのデバイスオブジェクトへのポインター。

<a href="" id="irpsp--parameters-verifyvolume-vpb"></a>*IrpSp- &gt; Parameters. VerifyVolume. Vpb*  
検証するボリュームの VPB へのポインター。

## <a name="see-also"></a>関連項目


[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状態 \_ ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






