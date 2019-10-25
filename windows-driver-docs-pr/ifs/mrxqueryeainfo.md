---
title: MRxQueryEaInfo ルーチン
description: MRxQueryEaInfo ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトの拡張属性情報を照会するように要求するために、RDBSS によって呼び出されます。
ms.assetid: 4471eb82-c176-4976-b722-5a6e067a7e69
keywords:
- MRxQueryEaInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryEaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75056b9a71e5fa8aba216b0df9297bf05154ba39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841088"
---
# <a name="mrxqueryeainfo-routine"></a>MRxQueryEaInfo ルーチン


*MRxQueryEaInfo*ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトの拡張属性情報を照会するように要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryEaInfo;

NTSTATUS MRxQueryEaInfo(
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

*MRxQueryEaInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><p>拡張属性情報を受信するバッファーが小さすぎます。</p>
<p>この戻り値は成功と見なす必要があり、可能な限り多くの有効なデータが、 <em>RxContext</em>パラメーターによって示される RX_CONTEXT 構造体の<strong>情報バッファー</strong>のメンバーに返される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>バッファーが小さすぎて要求されたデータを受け取ることができません。</p>
<p>この値が返される場合、 <em>RxContext</em>パラメーターが指す RX_CONTEXT 構造体の<strong>InformationToReturn</strong>メンバーは、呼び出しが成功するために必要なバッファーの最小サイズに設定されている必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_EA_CORRUPT_ERROR</strong></td>
<td align="left"><p>リモートサーバーから無効な拡張属性情報を受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NONEXISTENT_EA_ENTRY</strong></td>
<td align="left"><p>ファイルオブジェクトに拡張属性がなく、ユーザーが拡張属性インデックスを指定しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>拡張属性はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>SRV_OPEN 構造体は接続されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REQUEST_ABORTED</strong></td>
<td align="left"><p>ネットワーク要求が中止されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_クエリ\_EA**](irp-mj-query-ea.md)要求の受信に応答して、 *MRxQueryEaInfo*への呼び出しを発行します。

*MRxQueryEaInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**情報バッファー**のメンバーは、i/o 要求パケットからのユーザーバッファーに設定されます。 このバッファーは、必要に応じて、RDBSS によって既にロックされています。

**LengthRemaining**メンバーは**irpsp-&gt;パラメーター**に設定されています。 quer.

**Querは、UserEaList**メンバーが**irpsp-&gt;パラメーター**に設定されています。 quer. ealist.

**Querの**メンバーは、 **irpsp-&gt;のパラメーター**に設定されています。これは、ユーザーが設定します。

この**メンバーは、** **irpsp-&gt;パラメーター**に設定されています。これは、querです。

**Irpsp-&gt;フラグ**に SL\_再起動\_スキャンビットがある場合、 **RestartScan**メンバーは0以外に設定されます。

**Irpsp-&gt;フラグ**に SL\_\_単一\_エントリビットが返される場合、**このメンバーは**0 以外の値に設定されます。

**Irpsp-&gt;フラグ**に SL\_インデックス\_指定されたビットがオンになっている場合、**指定さ**れたメンバーは0以外に設定されます。

成功した場合、 *MRxQueryEaInfo*は RX\_コンテキスト構造の LengthRemaininging メンバーを、返された拡張属性情報の長さに設定し、さらに**fobx-&gt;OffsetOfNextEaToReturn**を更新する必要があり**ます。** レプリカ. *MRxQueryEaInfo*への呼び出しが成功した場合、RDBSS は、IRP の**Iostatus. 情報**メンバーを**irpsp-&gt;パラメーターに設定します**。また、RX\_コンテキストの**LengthRemaining**メンバーを差し引いてください。

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

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






