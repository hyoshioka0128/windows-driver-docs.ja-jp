---
title: FSCTL_DELETE_REPARSE_POINT 制御コード
description: FSCTL\_DELETE\_再解析\_ポイント制御コードは、指定されたファイルまたはディレクトリから再解析ポイントを削除します。 FSCTL\_DELETE\_再解析\_ポイントは、ファイルまたはディレクトリを削除しません。
ms.assetid: c8a06477-457b-47e5-b5c5-48d798fe08b3
keywords:
- FSCTL_DELETE_REPARSE_POINT 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_DELETE_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 303137d7fb5e9ad1f96aa365c0a8a79fe62c54c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841322"
---
# <a name="fsctl_delete_reparse_point-control-code"></a>FSCTL\_\_再解析\_ポイント制御コードを削除します


FSCTL\_DELETE\_再解析\_ポイント制御コードは、指定されたファイルまたはディレクトリから再解析ポイントを削除します。 FSCTL\_DELETE\_再解析\_ポイントは、ファイルまたはディレクトリを削除しません。

この操作を実行するには、次のパラメーターを使用して[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

再解析ポイントを削除するには、ミニフィルターで FSCTL\_DELETE\_再解析\_ポイントではなく[**Fltuntagfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)を使用する必要があります。

再解析ポイントおよび FSCTL\_DELETE\_再解析\_ポイント制御コードの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
再解析ポイントの削除元となるファイルまたはディレクトリのファイルハンドル。 呼び出し元には、ファイルまたはディレクトリへの書き込みアクセス権が必要です。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作では、FSCTL\_使用して\_再解析\_ポイントを削除します。

<a href="" id="inputbuffer"></a>*InputBuffer*  
データ\_バッファーまたは[**再解析\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)構造[ **\_\_GUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)へのポインター。 この構造体の**ReparseTag**メンバーで指定されるタグは、削除する再解析ポイントのタグと一致する必要があり、 **ReparseDataLength**メンバーはゼロである必要があります。 また、再解析ポイントがサードパーティ (Microsoft 以外) の再解析ポイントである場合は、再解析\_GUID\_データ\_バッファー構造の**ReparseGuid**メンバーに指定された guid が、削除する再解析ポイントの guid と一致している必要があります。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
**InputBuffer**パラメーターによってポイントされるバッファーのサイズ (バイト単位)。 再解析\_GUID\_データ\_バッファー構造の場合、この値は\_GUID\_データ\_バッファー\_のヘッダー\_サイズに正確に再解析する必要があります。 データ\_バッファー構造の再解析\_場合、この値は\_データ\_バッファー\_ヘッダー\_サイズに正確に再解析する必要があります。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような状態\_SUCCESS または適切な NTSTATUS 値を返します。

<a href="" id="status-io-reparse-data-invalid"></a>状態\_IO\_再解析\_データ\_無効  
指定されたパラメーター値の1つが無効です。 これはエラーコードです。

<a href="" id="status-io-reparse-tag-invalid"></a>状態\_IO\_再解析\_タグ\_無効  
呼び出し元によって指定された再解析タグが無効です。 これはエラーコードです。

<a href="" id="status-io-reparse-tag-mismatch"></a>状態\_IO\_再解析\_タグ\_不一致  
呼び出し元によって指定された再解析タグが、削除する再解析ポイントのタグと一致しませんでした。 これはエラーコードです。

<a href="" id="status-reparse-attribute-conflict"></a>ステータス\_再解析\_属性\_競合  
再解析ポイントはサードパーティの再解析ポイントであり、呼び出し元によって指定された再解析 GUID が、削除する再解析ポイントの GUID と一致しませんでした。 これはエラーコードです。

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

[**FSCTL\_\_再解析\_ポイントを取得します**](fsctl-get-reparse-point.md)

[**FSCTL\_設定\_再解析\_ポイント**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**データ\_バッファーの再解析\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_GUID\_データ\_バッファーの再解析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






