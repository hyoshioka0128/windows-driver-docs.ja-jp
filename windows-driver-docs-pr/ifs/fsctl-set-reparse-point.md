---
title: FSCTL_SET_REPARSE_POINT 制御コード
description: 再解析\_ポイント制御コード\_設定された FSCTL\_は、ファイルまたはディレクトリの再解析ポイントを設定します。
ms.assetid: db38cc62-845e-4690-a430-a9c834382b56
keywords:
- FSCTL_SET_REPARSE_POINT 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: f8f775fab2d807a393dfcd0d8663b124eec45c45
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841244"
---
# <a name="fsctl_set_reparse_point-control-code"></a>FSCTL\_\_再解析\_ポイント制御コードの設定


再解析\_ポイント制御コード\_設定された FSCTL\_は、ファイルまたはディレクトリの再解析ポイントを設定します。

この操作を実行するには、次のパラメーターを使用して[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

再解析ポイントを設定するには、FSCTL\_SET\_の代わりに[**Flttagfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)を使用して再解析\_ポイントを設定する必要があります。

再解析ポイントと FSCTL\_設定\_再解析\_ポイント制御コードの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
再解析ポイントを設定するファイルまたはディレクトリのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作では、FSCTL\_使用して、再解析\_ポイント\_設定します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
再解析ポイントデータを格納しているバッファー構造\_データ\_バッファーまたは[**再解析\_\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)を格納する、呼び出し元によって割り当てられた[**再解析\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)を指すポインター。 既存の再解析ポイントが変更されている場合は、この構造体の**ReparseTag**メンバーに指定されているタグが、変更する再解析ポイントのタグと一致している必要があります。 また、再解析ポイントがサードパーティ (Microsoft 以外) の再解析ポイントである場合、構造体の**ReparseGuid**メンバーに指定されている GUID は再解析\_GUID\_データ\_バッファー構造は再解析ポイントの guid と一致している必要があります変更する。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*パラメーターによってポイントされるバッファーのサイズ (バイト単位)。 再解析\_GUID\_データ\_バッファー構造体の場合、この値には少なくとも、GUID\_データ\_バッファー\_の\_のサイズとユーザー定義データのサイズを加えた再解析\_GUID を指定する必要があります。、\_再解析\_データ\_バッファー\_サイズの最大値以下である必要があります。 再解析\_データ\_バッファー構造の場合、この値は\_少なくともデータ\_バッファー\_のヘッダー\_サイズに加え、ユーザー定義データのサイズに加えて、最大値以下である必要があり\_再解析\_データ\_バッファー\_サイズ。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような状態\_SUCCESS または適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_DIRECTORY_NOT_EMPTY</strong></p></td>
<td align="left"><p>空でないディレクトリに再解析ポイントを設定することはできません。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_EAS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>この要求がトランザクション内にある場合、ファイルに再解析ポイントを設定することはできません。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定されたパラメーター値の1つが無効です。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_IO_REPARSE_TAG_MISMATCH</strong></p></td>
<td align="left"><p>呼び出し元によって指定された再解析タグが、変更する再解析ポイントのタグと一致しませんでした。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>ファイルまたはディレクトリが再解析ポイントではありません。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_REPARSE_ATTRIBUTE_CONFLICT</strong></p></td>
<td align="left"><p>再解析ポイントはサードパーティの再解析ポイントであり、呼び出し元によって指定された再解析 GUID が、変更する再解析ポイントの GUID と一致しませんでした。 これはエラーコードです。</p></td>
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


[**IRP\_MJ\_ファイルの FLT\_パラメーター\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_\_再解析\_ポイントを削除します**](fsctl-delete-reparse-point.md)

[**FSCTL\_\_再解析\_ポイントを取得します**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**データ\_バッファーの再解析\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_GUID\_データ\_バッファーの再解析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






