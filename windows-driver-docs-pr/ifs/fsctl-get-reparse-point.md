---
title: FSCTL_GET_REPARSE_POINT 制御コード
description: FSCTL\_取得\_再解析\_ポイント制御コードを指定したファイルまたはディレクトリに関連付けられている再解析ポイントのデータを取得します。
ms.assetid: 8d56a4c5-46c3-42b7-a532-eaf0d792b519
keywords:
- FSCTL_GET_REPARSE_POINT 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 0c935357f6ce270037409c71e57e3324945098f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327892"
---
# <a name="fsctlgetreparsepoint-control-code"></a>FSCTL\_取得\_再解析\_ポイント制御コード


FSCTL\_取得\_再解析\_ポイント制御コードを指定したファイルまたはディレクトリに関連付けられている再解析ポイントのデータを取得します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

再解析ポイントと FSCTL の詳細については\_取得\_再解析\_ポイント制御コードを Microsoft Windows SDK のマニュアルを参照してください。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 ファイルまたはディレクトリから、再解析ポイントのデータを取得する対象のファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ファイルまたはディレクトリから、再解析ポイントのデータを取得する対象のファイル ハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_取得\_再解析\_ポイント**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。0 に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
呼び出し元が割り当てたへのポインター [**再解析\_GUID\_データ\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff552014)または[**再解析\_データ\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff552012)再解析ポイントのデータを受信する構造体。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
指し示されるバッファーのバイト単位のサイズ、 *OutputBuffer*パラメーター。 再解析の\_GUID\_データ\_バッファーの構造体は、この値は、以上である必要があります**sizeof**(再解析\_GUID\_データ\_バッファー\_ヘッダー\_サイズ)、必要なユーザー定義データのサイズは最大値以下である必要がありますプラス\_再解析\_データ\_バッファー\_サイズ。 再解析の\_データ\_バッファーの構造体は、この値は、以上である必要があります**sizeof**(再解析\_データ\_バッファー\_ヘッダー\_サイズ)、さらのサイズ予想されるユーザー定義データは最大値以下である必要があります\_再解析\_データ\_バッファー\_サイズ。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_成功、または、次のいずれかなどの適切な NTSTATUS 値。

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
<td align="left"><p>バッファーを<em>OutputBuffer</em>にパラメーターが指すは REPARSE_GUID_DATA_BUFFER または REPARSE_DATA_BUFFER 構造データではなく、ユーザー定義の固定部分を保持するために十分な大きさです。 再解析ポイントのデータの固定部分のみが返されるここで、 <em>OutputBuffer</em>バッファー。 <em>LengthReturned</em>パラメーターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff542988" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542988)"> <strong>FltFsControlFile</strong> </a>返されるデータのバイト単位で実際の長さを受信します。 これは、警告コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>バッファーを<em>OutputBuffer</em>パラメーターが指しては再解析ポイントのデータを保持するのに十分な大きさがありません。 <em>LengthReturned</em>パラメーターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff542988" data-raw-source="[&lt;strong&gt;FltFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542988)"> <strong>FltFsControlFile</strong> </a> (または<strong>情報</strong>のメンバー、 <em>IoStatus</em>パラメーターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff566462" data-raw-source="[&lt;strong&gt;ZwFsControlFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566462)"> <strong>ZwFsControlFile</strong></a>) 必要なバッファー サイズを受け取ります。 この場合、再解析ポイントのデータは返されません。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_IO_REPARSE_DATA_INVALID</strong></p></td>
<td align="left"><p>指定されたパラメーター値のいずれかが無効です。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_NOT_A_REPARSE_POINT</strong></p></td>
<td align="left"><p>ファイルまたはディレクトリは、再解析ポイントではありません。 これは、エラー コードです。</p></td>
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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IRP のパラメーター\_MJ\_ファイル\_システム\_コントロール**](flt-parameters-for-irp-mj-file-system-control.md)

[**FLT\_タグ\_データ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff544820)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FltTagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544589)

[**FltUntagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544608)

[**FSCTL\_DELETE\_REPARSE\_POINT**](fsctl-delete-reparse-point.md)

[**FSCTL\_SET\_REPARSE\_POINT**](fsctl-set-reparse-point.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IsReparseTagMicrosoft**](https://msdn.microsoft.com/library/windows/hardware/ff549452)

[**IsReparseTagNameSurrogate**](https://msdn.microsoft.com/library/windows/hardware/ff549462)

[**再解析\_データ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff552012)

[**再解析\_GUID\_データ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff552014)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






