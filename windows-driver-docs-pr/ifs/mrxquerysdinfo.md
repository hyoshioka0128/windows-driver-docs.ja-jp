---
title: MRxQuerySdInfo ルーチン
description: TheMRxQuerySdInfo ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を照会するように要求するために、RDBSS によって呼び出されます。
ms.assetid: 5bab05f1-2a79-42c0-ba70-e1124f7b1528
keywords:
- MRxQuerySdInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQuerySdInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a207efdd43553fd209f4c991ccb9bde7be30d74
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841084"
---
# <a name="mrxquerysdinfo-routine"></a>MRxQuerySdInfo ルーチン


*MRxQuerySdInfo*ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのセキュリティ記述子情報を照会するように要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQuerySdInfo;

NTSTATUS MRxQuerySdInfo(
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

*MRxQuerySdInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><p>セキュリティ記述子の情報を受信するバッファーが小さすぎます。</p>
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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワークアクセスが拒否されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモートページファイルの情報など、要求された機能は実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>セキュリティ記述子の情報は、リモート共有ではサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリームオブジェクトの情報が要求され、リモートファイルシステムでストリームがサポートされていない場合に返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリックリンクを処理するには、再解析が必要です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)要求の受信に応答して、 *MRxQuerySdInfo*への呼び出しを発行します。

*MRxQuerySdInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**Querysecurity. securityinformation**メンバーは、 **irpsp-&gt;Parameters. Querysecurity. securityinformation**に設定されています。

**情報バッファー**のメンバーは、i/o 要求パケットからのユーザーバッファーに設定されます。 このバッファーは、必要に応じて、RDBSS によって既にロックされています。

**LengthRemaining**メンバーは**irpsp-&gt;Parameters. Querysecurity. Length**に設定されています。

成功した場合、ネットワークミニリダイレクターは、RX\_コンテキスト構造の**InformationToReturn**メンバーを、返されたセキュリティ情報の長さに設定する必要があります。 *MRxQuerySdInfo*への呼び出しが成功した場合、RDBSS は IRP の**Iostatus. 情報**メンバーを RX\_コンテキストの**InformationToReturn**メンバーに設定します。

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

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






