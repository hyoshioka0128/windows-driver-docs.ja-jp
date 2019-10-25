---
title: MRxQueryFileInfo ルーチン
description: TheMRxQueryFileInfo ルーチンは RDBSS によって呼び出され、ネットワークミニリダイレクターがファイルシステムオブジェクトのファイル情報を照会するよう要求します。
ms.assetid: 201b749c-527b-4c02-a860-d2f54777dc32
keywords:
- MRxQueryFileInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryFileInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982ad1abf13c3115cf3593b764d96b043eee5013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841090"
---
# <a name="mrxqueryfileinfo-routine"></a>MRxQueryFileInfo ルーチン


*MRxQueryFileInfo*ルーチンは[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出され、ネットワークミニリダイレクターがファイルシステムオブジェクトのファイル情報を照会するよう要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryFileInfo;

NTSTATUS MRxQueryFileInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryFileInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>呼び出し元には、この操作に対する適切なセキュリティが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>ファイル情報を受信するバッファーが小さすぎます。</p>
<p>この戻り値は成功と見なす必要があり、可能な限り多くの有効なデータが、 <em>RxContext</em>パラメーターによって示される RX_CONTEXT 構造体の<strong>情報バッファー</strong>のメンバーに返される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>バッファーが小さすぎて要求されたデータを受け取ることができません。</p>
<p>この値が返される場合、 <em>RxContext</em>パラメーターが指す RX_CONTEXT 構造体の<strong>InformationToReturn</strong>メンバーは、呼び出しが成功するために必要なバッファーの最小サイズに設定されている必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>リモートサーバーから無効なファイル情報バッファーを受け取りました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p>
<p>この値は、RX_CONTEXT の<strong>Fileinformationclass</strong>メンバーに無効な値が渡された場合に返されます。 この値は、指定された<strong>Fileinformationclass</strong>メンバーが<strong>FileStreamInformation</strong>用であり、リモートファイルシステムでストリームがサポートされていない場合にも返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクト名が見つかりませんでした。 これはエラーコードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)要求の受信に応答して、 *MRxQueryFileInfo*への呼び出しを発行します。

*MRxQueryFileInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**Info. fileinformationclass**メンバーは、 **irpsp-&gt;Parameters. Queryfile. fileinformationclass**に設定され、要求されたファイル\_情報\_クラス値に設定されます。

**情報バッファー**のメンバーは、i/o 要求パケットからのユーザーバッファーに設定されます。

**LengthRemaining**メンバーは、 **irpsp-&gt;Parameters. Queryfile. の値**に設定されます。

**Querydirectory. fileindex**メンバーは**irpsp-&gt;Parameters. Querydirectory. fileindex**に設定されます。

**Irpsp-&gt;フラグ**に SL\_再起動\_スキャンビットが設定されている場合は、 **RestartScan**メンバーが設定されます。

**Irpsp-&gt;フラグ**が SL を持つ場合は、 **Querydirectory. returnsingleentry**メンバーが設定され\_単一\_エントリビットセットが返さ\_ます。

UnicodeQueryTemplate が**NULL**で fobx **&gt;フラグ**に FOBX\_フラグが設定されていない **&gt;** 場合は、 **querydirectory. initialquery**メンバーが設定されます。これは、すべてのビットセット\_\_一致しません。

成功した場合、ネットワークミニリダイレクターは、RX\_コンテキスト構造の**LengthRemaining**メンバーを、返されたファイル情報の長さを差し引いた**値に設定する必要**があります。 *MRxQueryFileInfo*への呼び出しが成功した場合、RDBSS は IRP の**Iostatus. 情報**メンバーを**irpsp-&gt;パラメーター**に設定します。 LengthRemaining メンバーから RX\_コンテキストの値を差し引いた値 **。**

RDBSS は、SL\_インデックス\_指定された、 **Irpsp-&gt;フラグ**が設定されている要求をサポートしていません。 ネットワークミニリダイレクターは、SL\_インデックス\_指定されている**Irpsp-&gt;フラグ**が設定された状態で、 *MRxQueryFileInfo*への呼び出しを受信しません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






