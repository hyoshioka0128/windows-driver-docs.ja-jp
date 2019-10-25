---
title: MRxQueryQuotaInfo ルーチン
description: MRxQueryQuotaInfo ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのクォータ情報を照会するように要求するために、RDBSS によって呼び出されます。
ms.assetid: 44bf976b-09bc-4270-8c2e-8e55784aaa38
keywords:
- MRxQueryQuotaInfo ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryQuotaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8801abd633bf8639c316b4afab032767d74022
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841087"
---
# <a name="mrxqueryquotainfo-routine"></a>MRxQueryQuotaInfo ルーチン


*MRxQueryQuotaInfo*ルーチンは、ネットワークミニリダイレクターがファイルシステムオブジェクトのクォータ情報を照会するように要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryQuotaInfo;

NTSTATUS MRxQueryQuotaInfo(
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

*MRxQueryQuotaInfo*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><p>クォータ情報を受信するバッファーが小さすぎます。</p>
<p>この戻り値は成功と見なす必要があり、可能な限り多くの有効なデータが、 <em>RxContext</em>パラメーターによって示される RX_CONTEXT 構造体の<strong>情報バッファー</strong>のメンバーに返される必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>バッファーが小さすぎて要求されたデータを受け取ることができません。</p>
<p>この値が返される場合、 <em>RxContext</em>パラメーターが指す RX_CONTEXT 構造体の<strong>InformationToReturn</strong>メンバーは、呼び出しが成功するために必要なバッファーの最小サイズに設定されている必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。 これはエラーコードです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。 これはエラーコードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>クォータはサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS は、 [**IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)要求の受信に応答して、 *MRxQueryQuotaInfo*への呼び出しを発行します。

*MRxQueryQuotaInfo*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**情報バッファー**のメンバーは、i/o 要求パケットからのユーザーバッファーに設定されます。 このバッファーは、必要に応じて、RDBSS によって既にロックされています。

**LengthRemaining**メンバーは**irpsp-&gt;Parameters. Queryquota. Length**に設定されています。

**Queryquota. sidlist**メンバーは**irpsp-&gt;Parameters. Queryquota. sidlist**に設定されています。

**Queryquota. sidlistlength**メンバーは、irpsp-&gt;パラメーターに設定されています。 **Queryquota. sidlistlength**。

**Queryquota. startsid**メンバーは**irpsp-&gt;Parameters. Queryquota. startsid**に設定されています。

**Queryquota. length**メンバーは、 **irpsp-&gt;Parameters. queryquota. length**に設定されています。

**Irpsp-&gt;フラグ**に SL\_再起動\_スキャンビットが設定されている場合、 **RestartScan**メンバーは0以外に設定されます。

**Irpsp-&gt;フラグ**に SL\_\_単一\_エントリビットセットが返される場合、**このメンバーは**0 以外の値に設定されます。

**Irpsp-&gt;フラグ**に SL\_インデックス\_指定されたビットセットがある場合、**指定さ**れたメンバーは0以外に設定されます。

成功した場合、ネットワークミニリダイレクターは、RX\_コンテキスト構造の**LengthRemaining**メンバーに、返されるクォータ情報の長さを設定する必要があります。 *MRxQueryQuotaInfo*への呼び出しが成功した場合、RDBSS は IRP の**Iostatus. 情報**メンバーを RX\_コンテキストの**LengthRemaining**メンバーに設定します。

*MRxQueryQuotaInfo*の呼び出しが成功した場合、RX\_コンテキスト構造の**InformationToReturn**メンバーは、返されるクォータ情報の長さに設定する必要があります。 呼び出しが失敗した場合は、RX\_コンテキストの**InformationToReturn**メンバーを0に設定する必要があります。

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

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






