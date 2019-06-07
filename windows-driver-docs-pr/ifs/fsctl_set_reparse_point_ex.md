---
title: FSCTL_SET_REPARSE_POINT_EX 制御コード
description: FSCTL_SET_REPARSE_POINT_EX 制御コードは、ファイルまたはディレクトリの再解析ポイントを設定します。
tech.root: ''
ms.assetid: 5867cbe3-5aab-43f8-b5bf-eaa29857359f
keywords:
- FSCTL_SET_REPARSE_POINT_EX 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_REPARSE_POINT_EX
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 05/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 459efeede95677838391c5f4c918a900d2c3f8f6
ms.sourcegitcommit: 2b60304fb0e33fd978ae01be95d04321a0af09b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748456"
---
# <a name="fsctlsetreparsepointex-control-code"></a>FSCTL_SET_REPARSE_POINT_EX 制御コード

FSCTL_SET_REPARSE_POINT_EX 制御コードは、ファイルまたはディレクトリの再解析ポイントを設定します。

ミニフィルターを使用する必要があります[ **FltTagFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfileex) FSCTL_SET_REPARSE_POINT_EX 再解析ポイントを設定する代わりにします。

再解析ポイントの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

この操作を実行するには、呼び出す[ **ZwFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile)次のパラメーターを使用します。

## <a name="parameters"></a>パラメーター

*FileHandle*  
ファイルまたはディレクトリを再解析ポイントを設定する対象のファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

*イベント*この操作で使用するに設定せず**NULL**します。

*ApcRoutine*この操作で使用するに設定せず**NULL**します。

*ApcContext*この操作で使用するに設定せず**NULL**します。

*IoStatusBlock*最終的な完了の状態と操作に関する情報を受信する IO_STATUS_BLOCK 構造へのポインター。

*FsControlCode*  
操作のコードを制御します。 この操作に FSCTL_SET_REPARSE_POINT_EX を使用します。

*InputBuffer*  
呼び出し元が割り当てたへのポインター [REPARSE_DATA_BUFFER_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer_ex)再解析ポイントのデータを含む構造体。

*InputBufferLength*  
指し示されるバッファーのバイト単位のサイズ、 *InputBuffer*パラメーター。 この値は以上である必要があります REPARSE_GUID_DATA_BUFFER_HEADER_SIZE とユーザー定義のデータのサイズは MAXIMUM_REPARSE_DATA_BUFFER_SIZE 未満である必要があります。

*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------
[**ZwFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile) STATUS_SUCCESS または、次のいずれかなどの適切な NTSTATUS 値を返します。

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

## <a name="requirements"></a>必要条件
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

[**FLT_PARAMETERS for IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control)

[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfileex)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**再解析\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer_ex)

[**再解析\_GUID\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntfscontrolfile)