---
title: FSCTL_DELETE_REPARSE_POINT 制御コード
description: FSCTL\_削除\_再解析\_ポイント制御コードは、指定したファイルまたはディレクトリから再解析ポイントを削除します。 FSCTL を使用して\_削除\_再解析\_ポイントでは、ファイルまたはディレクトリは削除されません。
ms.assetid: c8a06477-457b-47e5-b5c5-48d798fe08b3
keywords:
- FSCTL_DELETE_REPARSE_POINT 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 4c4e03922410f8569a8b1060ca9cd54ba6638880
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365070"
---
# <a name="fsctldeletereparsepoint-control-code"></a>FSCTL\_削除\_再解析\_ポイント制御コード


FSCTL\_削除\_再解析\_ポイント制御コードは、指定したファイルまたはディレクトリから再解析ポイントを削除します。 FSCTL を使用して\_削除\_再解析\_ポイントでは、ファイルまたはディレクトリは削除されません。

この操作を実行するには、呼び出す[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

ミニフィルターを使用する必要があります[ **FltUntagFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile) FSCTL ではなく\_削除\_再解析\_再解析ポイントを削除するポイント。

再解析ポイントと FSCTL の詳細については\_削除\_再解析\_ポイント制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="filehandle"></a>*FileHandle*  
ファイルまたはディレクトリの再解析ポイントの削除元のファイル ハンドル。 呼び出し元のファイルまたはディレクトリへの書き込みアクセスが必要です。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作のコードを制御します。 FSCTL を使用して、\_削除\_再解析\_この操作にポイントします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
ポインターを[**再解析\_GUID\_データ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)または[**再解析\_データ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)構造体。 指定されたタグ、 **ReparseTag**この構造体のメンバーは、削除する再解析ポイントのタグと一致する必要があります、 **ReparseDataLength**メンバーは 0 である必要があります。 さらに、再解析ポイントがサードパーティ (Microsoft 以外の) 再解析ポイントの場合は、GUID はで指定された、 **ReparseGuid** 、再解析のメンバー\_GUID\_データ\_バッファーの構造が一致する必要があります、再解析の GUID は、削除をポイントします。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
指し示されるバッファーのバイト単位のサイズ、 **InputBuffer**パラメーター。 再解析の\_GUID\_データ\_バッファーの構造体は、この値は正確に再解析する必要があります\_GUID\_データ\_バッファー\_ヘッダー\_サイズ。 再解析の\_データ\_バッファーの構造体は、この値は正確に再解析する必要があります\_データ\_バッファー\_ヘッダー\_サイズ。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値。

<a href="" id="status-io-reparse-data-invalid"></a>STATUS\_IO\_REPARSE\_DATA\_INVALID  
指定されたパラメーター値のいずれかが無効です。 これは、エラー コードです。

<a href="" id="status-io-reparse-tag-invalid"></a>STATUS\_IO\_REPARSE\_TAG\_INVALID  
呼び出し元によって指定された再解析タグが無効です。 これは、エラー コードです。

<a href="" id="status-io-reparse-tag-mismatch"></a>STATUS\_IO\_REPARSE\_TAG\_MISMATCH  
呼び出し元によって指定された再解析タグでは、削除する再解析ポイントのタグが一致しませんでした。 これは、エラー コードです。

<a href="" id="status-reparse-attribute-conflict"></a>ステータス\_再解析\_属性\_競合  
再解析ポイントは、サード パーティ製の再解析ポイントと、再解析、呼び出し元によって指定された GUID と一致しませんでした再解析ポイントの GUID を削除します。 これは、エラー コードです。

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

[**FSCTL\_GET\_REPARSE\_POINT**](fsctl-get-reparse-point.md)

[**FSCTL\_SET\_REPARSE\_POINT**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**再解析\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_data_buffer)

[**再解析\_GUID\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






