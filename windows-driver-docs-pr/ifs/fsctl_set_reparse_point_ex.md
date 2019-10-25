---
title: FSCTL_SET_REPARSE_POINT_EX 制御コード
description: FSCTL_SET_REPARSE_POINT_EX 制御コードは、ファイルまたはディレクトリに再解析ポイントを設定します。
tech.root: ''
ms.assetid: 5867cbe3-5aab-43f8-b5bf-eaa29857359f
keywords:
- FSCTL_SET_REPARSE_POINT_EX 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 44801354f6c37c8540b9e88ca50420f97f782b2c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841236"
---
# <a name="fsctl_set_reparse_point_ex-control-code"></a>FSCTL_SET_REPARSE_POINT_EX 制御コード

FSCTL_SET_REPARSE_POINT_EX 制御コードは、ファイルまたはディレクトリに再解析ポイントを設定します。

ミニフィルターでは、再解析ポイントを設定するために FSCTL_SET_REPARSE_POINT_EX ではなく[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfileex)を使用する必要があります。

再解析ポイントの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

この操作を実行するには、次のパラメーターを使用して[**Zwfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile)を呼び出します。

## <a name="parameters"></a>パラメーター

*FileHandle*  
再解析ポイントを設定するファイルまたはディレクトリのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

*イベント*この操作では使用されません。を**NULL**に設定します。

*Apcroutine*この操作では使用されません。を**NULL**に設定します。

*Apccontext*この操作では使用されません。を**NULL**に設定します。

*Iostatusblock*最終的な完了状態と操作に関する情報を受け取る IO_STATUS_BLOCK 構造体へのポインター。

*FsControlCode*  
操作の制御コード。 この操作には FSCTL_SET_REPARSE_POINT_EX を使用します。

*InputBuffer*  
再解析ポイントデータを含む、呼び出し元によって割り当てられた[REPARSE_DATA_BUFFER_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex)構造体へのポインター。

*InputBufferLength*  
*InputBuffer*パラメーターによってポイントされるバッファーのサイズ (バイト単位)。 この値は、少なくとも REPARSE_GUID_DATA_BUFFER_HEADER_SIZE で、ユーザー定義データのサイズに加えて、MAXIMUM_REPARSE_DATA_BUFFER_SIZE 以下である必要があります。

*OutputBuffer*  
この操作では使用されません。を**NULL**に設定します。

*OutputBufferLength*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------
[**Zwfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile)は、次のいずれかのような STATUS_SUCCESS または適切な NTSTATUS 値を返します。

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

## <a name="requirements"></a>要件
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

[**IRP_MJ_FILE_SYSTEM_CONTROL の FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-file-system-control)

[**FltTagFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfileex)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_\_再解析\_ポイントを削除します**](fsctl-delete-reparse-point.md)

[**FSCTL\_\_再解析\_ポイントを取得します**](fsctl-get-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**データ\_バッファーの再解析\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer_ex)

[ **\_GUID\_データ\_バッファーの再解析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntfscontrolfile)