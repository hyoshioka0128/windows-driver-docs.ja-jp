---
title: FSCTL_GET_REPARSE_POINT 制御コード
description: FSCTL\_GET\_再解析\_ポイント制御コードは、指定したファイルまたはディレクトリに関連付けられている再解析ポイントデータを取得します。
ms.assetid: 8d56a4c5-46c3-42b7-a532-eaf0d792b519
keywords:
- FSCTL_GET_REPARSE_POINT 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_REPARSE_POINT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e53ba6d929805baa9d704f532fd0d12870814851
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841306"
---
# <a name="fsctl_get_reparse_point-control-code"></a>FSCTL\_\_再解析\_ポイント制御コードを取得します


FSCTL\_GET\_再解析\_ポイント制御コードは、指定したファイルまたはディレクトリに関連付けられている再解析ポイントデータを取得します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

再解析ポイントおよび FSCTL\_GET\_再解析\_ポイント制御コードの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 再解析ポイントデータの取得元となるファイルまたはディレクトリのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 再解析ポイントデータの取得元となるファイルまたはディレクトリのファイルハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作を行うには、FSCTL\_使用して **\_再解析\_ポイントを取得**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。を**NULL**に設定します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。を0に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
再解析ポイントデータを受け取るバッファー構造体[ **\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)または[**再\_\_解析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)\_GUID を指すポインター。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*Outputbuffer*パラメーターが指すバッファーのサイズ (バイト単位)。 再解析\_GUID\_データ\_バッファー構造体の場合、この値には少なくとも、\_データ\_バッファー\_のデータ\_サイズ、および予期されるユーザー定義データのサイズに対する再解析\_GUID を指定する必要があります。、\_再解析\_データ\_バッファー\_サイズの最大値以下である必要があります。 再解析\_データ\_バッファー構造体の場合、この値は\_少なくともデータ\_バッファー\_のヘッダー\_サイズに加えて、予想されるユーザー定義データのサイズに加え、最大値以下である必要があり\_再解析\_データ\_バッファー\_サイズ。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、次のいずれかのような状態\_SUCCESS または適切な NTSTATUS 値を返します。

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
<td align="left"><p><strong>STATUS_BUFFER_OVERFLOW</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>パラメーターが指すバッファーは、REPARSE_GUID_DATA_BUFFER または REPARSE_DATA_BUFFER 構造体の固定部分を保持するのに十分な大きさですが、ユーザー定義データは保持できません。 この場合は、再解析ポイントデータの固定部分のみが<em>outputbuffer</em>バッファーに返されます。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>Fltfscontrolfile</strong></a>に<em>返され</em>た長さのパラメーターは、返されたデータの実際の長さをバイト単位で受け取ります。 これは警告コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>Outputbuffer</em>パラメーターが指すバッファーが、再解析ポイントデータを保持するのに十分な大きさではありません。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)"><strong>Fltfscontrolfile</strong></a>に<em>返された長さ</em>(または、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566462" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566462)"><strong>Iowfscontrolfile</strong></a>への<em>iostatus</em>パラメーターの<strong>情報</strong>メンバー) は、必要なバッファーサイズを受け取ります。 この場合、再解析ポイントデータは返されません。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定されたパラメーター値の1つが無効です。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>ファイルまたはディレクトリが再解析ポイントではありません。 これはエラーコードです。</p></td>
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

[**FLT\_タグ\_データ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_tag_data_buffer)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

[**FSCTL\_\_再解析\_ポイントを削除します**](fsctl-delete-reparse-point.md)

[**FSCTL\_設定\_再解析\_ポイント**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagmicrosoft)

[**IsReparseTagNameSurrogate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-isreparsetagnamesurrogate)

[**データ\_バッファーの再解析\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_data_buffer)

[ **\_GUID\_データ\_バッファーの再解析**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_reparse_guid_data_buffer)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






