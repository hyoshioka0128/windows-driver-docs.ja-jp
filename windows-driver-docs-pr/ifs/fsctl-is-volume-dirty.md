---
title: FSCTL_IS_VOLUME_DIRTY 制御コード
description: FSCTL\_IS\_ボリューム\_ダーティ制御コードは、指定されたボリュームがダーティかどうかを判断します。
ms.assetid: 77263957-cf7f-4db1-81b7-c58438202518
keywords:
- FSCTL_IS_VOLUME_DIRTY 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: bbdf6b3988fceac7c1f0477e4aab30add8df74c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380148"
---
# <a name="fsctlisvolumedirty-control-code"></a>FSCTL\_IS\_ボリューム\_ダーティ制御コード


**FSCTL\_IS\_ボリューム\_DIRTY**制御コードは、指定されたボリュームがダーティかどうかを判断します。

NTFS が状態を返す場合は、ボリュームの情報ファイルが破損している\_ファイル\_が壊れています\_エラー。

ミニフィルター ドライバーの呼び出しは、この操作を実行する[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)の次のパラメーターとファイル システム リダイレクター、および従来のファイル システム フィルター ドライバー呼び出し[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ボリュームのファイル オブジェクト ポインター。 このパラメーターは、マウントされたファイル システム ボリュームのユーザーのボリュームのオープンを表す必要があります。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ボリュームの処理です。 このパラメーターは、マウントされているファイル システム ボリュームのユーザー ボリューム オープンのハンドルを指定する必要があります。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作のコードを制御します。 FSCTL を使用して、\_IS\_ボリューム\_この操作に面倒です。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。0 に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
ボリュームが現在ダーティかどうかを示すフラグの ULONG ビットマスクを受け取る呼び出し元が割り当てた、32 ビット アライン バッファーへのポインター。 1 つ以上の次の表に、フラグを設定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VOLUME_IS_DIRTY</p></td>
<td align="left"><p>ボリュームがダーティです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VOLUME_UPGRADE_SCHEDULED</p></td>
<td align="left"><p>この値は現在は使用されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>その他のすべての値</p></td>
<td align="left"><p>将来使用するために予約されています。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指すバッファーのバイト単位のサイズ、 *OutputBuffer*パラメーター。 このサイズは以上である必要があります sizeof(ULONG) します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では、次の NTSTATUS 値のいずれかを返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOURCES</strong></p></td>
<td align="left"><p>ファイル システムには、プールの割り当てエラーが発生しました。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>バッファーを<em>OutputBuffer</em>にパラメーターが指すは<strong>NULL</strong>、または<em>FileHandle</em>または<em>FileObject</em>パラメーターが表すありませんユーザー ボリュームを開きます。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_USER_BUFFER</strong></p></td>
<td align="left"><p>バッファーを<em>OutputBuffer</em>を指しますが、再解析ポイントのデータを保持するために十分な大きさでない、または<em>FileHandle</em>または<em>FileObject</em>パラメーターはありませんユーザーのボリュームのオープンを表します。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_VOLUME_DISMOUNTED</strong></p></td>
<td align="left"><p>ボリュームがマウントされていません。 これは、エラー コードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






