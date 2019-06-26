---
title: FSCTL_SET_REPARSE_POINT 制御コード
description: FSCTL\_設定\_再解析\_ポイント制御コードは、ファイルまたはディレクトリの再解析ポイントを設定します。
ms.assetid: db38cc62-845e-4690-a430-a9c834382b56
keywords:
- FSCTL_SET_REPARSE_POINT 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4d978a6c2cc57370599c020430371cf7dfd98c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366237"
---
# <a name="fsctlsetreparsepoint-control-code"></a>FSCTL\_設定\_再解析\_ポイント制御コード


FSCTL\_設定\_再解析\_ポイント制御コードは、ファイルまたはディレクトリの再解析ポイントを設定します。

この操作を実行するには、呼び出す[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

ミニフィルターを使用する必要があります[ **FltTagFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile) FSCTL ではなく\_設定\_再解析\_再解析ポイントを設定するポイント。

再解析ポイントと FSCTL の詳細については\_設定\_再解析\_ポイント制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
ファイルまたはディレクトリを再解析ポイントを設定する対象のファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作のコードを制御します。 FSCTL を使用して、\_設定\_再解析\_この操作にポイントします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
呼び出し元が割り当てたへのポインター [**再解析\_GUID\_データ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)または[**再解析\_データ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)再解析ポイントのデータを含む構造体。 タグが指定された既存の再解析ポイントが変更されている場合、 **ReparseTag**この構造体のメンバーが変更される再解析ポイントのタグと一致する必要があります。 さらに、再解析ポイントがサードパーティ (Microsoft 以外の) 再解析ポイントの場合は、GUID はで指定された、 **ReparseGuid** 、構造体のメンバーは、再解析\_GUID\_データ\_バッファーの構造体変更する再解析ポイントの GUID が一致する必要があります。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
指し示されるバッファーのバイト単位のサイズ、 *InputBuffer*パラメーター。 再解析の\_GUID\_データ\_バッファーの構造体は、この値がある必要がありますには少なくとも再解析\_GUID\_データ\_バッファー\_ヘッダー\_のサイズの合計サイズユーザー定義のデータとは最大値以下である必要があります\_再解析\_データ\_バッファー\_サイズ。 再解析の\_データ\_バッファーの構造体は、この値がある必要があります少なくとも再解析\_データ\_バッファー\_ヘッダー\_サイズ、さらに、ユーザー定義データのサイズとする必要がありますより小さいか、最大値に等しい\_再解析\_データ\_バッファー\_サイズ。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値。

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
<td align="left"><p><strong>STATUS_DIRECTORY_NOT_EMPTY</strong></p></td>
<td align="left"><p>再解析ポイントは、空でないディレクトリに設定できません。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_EAS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>再解析ポイントは、この要求が、トランザクションの場合、ファイルを設定できません。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定されたパラメーター値のいずれかが無効です。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_IO_REPARSE_TAG_MISMATCH</strong></p></td>
<td align="left"><p>呼び出し元によって指定された再解析タグでは、変更する再解析ポイントのタグが一致しませんでした。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>ファイルまたはディレクトリは、再解析ポイントではありません。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_REPARSE_ATTRIBUTE_CONFLICT</strong></p></td>
<td align="left"><p>再解析ポイントは、サード パーティ製の再解析ポイントと、再解析、呼び出し元によって指定された GUID と一致しませんでした変更する再解析ポイントの GUID。 これは、エラー コードです。</p></td>
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


[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**再解析\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)

[**再解析\_GUID\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






