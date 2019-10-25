---
title: FSCTL_IS_VOLUME_DIRTY 制御コード
description: FSCTL\_は\_ボリューム\_ダーティコントロールコードによって、指定されたボリュームがダーティかどうかが判断されます。
ms.assetid: 77263957-cf7f-4db1-81b7-c58438202518
keywords:
- FSCTL_IS_VOLUME_DIRTY 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_IS_VOLUME_DIRTY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa38c11230bff83b14a02ac7c03411ac26e54cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841294"
---
# <a name="fsctl_is_volume_dirty-control-code"></a>FSCTL\_は\_ボリューム\_ダーティコントロールコード


**FSCTL\_は\_ボリューム\_ダーティ**コントロールコードによって、指定されたボリュームがダーティかどうかが判断されます。

ボリューム情報ファイルが破損している場合は、NTFS によってステータス\_ファイル\_破損\_エラーが返されます。

この操作を実行するには、ミニフィルタードライバーは、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)を呼び出します。ファイルシステム、リダイレクター、およびレガシファイルシステムフィルタードライバーは、次のパラメーターを使用して[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ボリュームのファイルオブジェクトポインター。 このパラメーターは、マウントされたファイルシステムボリュームを開いているユーザーボリュームを表す必要があります。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ボリュームのハンドル。 このパラメーターは、マウントされたファイルシステムボリュームを開いているユーザーボリュームのハンドルである必要があります。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作では、ボリューム\_ダーティ\_\_を使用します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。を0に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
ボリュームが現在ダーティであるかどうかを示すフラグの ULONG ビットマスクを受け取る、呼び出し元が割り当てた32ビットのアラインされたバッファーへのポインター。 次の表に示す1つ以上のフラグを設定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VOLUME_IS_DIRTY</p></td>
<td align="left"><p>ボリュームがダーティです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VOLUME_UPGRADE_SCHEDULED</p></td>
<td align="left"><p>この値は現在使用されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他のすべての値</p></td>
<td align="left"><p>将来使用するために予約されています。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターによってポイントされるバッファーのサイズ (バイト単位)。 このサイズは、少なくとも sizeof (ULONG) である必要があります。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>ファイルシステムでプール割り当てエラーが発生しました。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>パラメーターが指すバッファーが<strong>NULL</strong>であるか、 <em>FileHandle</em>または<em>FileObject</em>パラメーターが、開いているユーザーボリュームを表していません。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>パラメーターが指すバッファーが、再解析ポイントデータを保持するのに十分な大きさではありません。または、 <em>FileHandle</em>または<em>FileObject</em>パラメーターが、開いているユーザーボリュームを表していません。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ボリュームがマウントされていません。 これはエラーコードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**IRP\_MJ\_ファイルの FLT\_パラメーター\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






