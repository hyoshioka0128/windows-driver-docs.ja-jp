---
title: MRxQueryQuotaInfo routine
description: MRxQueryQuotaInfo ルーチンによって呼び出されます RDBSS 要求をネットワーク ミニリダイレクター クエリ クォータについては、ファイル システム オブジェクト。
ms.assetid: 44bf976b-09bc-4270-8c2e-8e55784aaa38
keywords:
- MRxQueryQuotaInfo ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: a4a33043e34bcd5cc4cd6a25b47378a59fe60daf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324464"
---
# <a name="mrxqueryquotainfo-routine"></a>MRxQueryQuotaInfo routine


*MRxQueryQuotaInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトのクォータ情報を照会することを要求します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryQuotaInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><p>呼び出し元には、この操作に適切なセキュリティが不足していました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>クォータ情報を受け取るバッファーが小さすぎます。</p>
<p>これは戻り値は、成功を考慮してでできるだけの非常に有効なデータとして返す必要がある、 <strong>Info.Buffer</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>要求されたデータを受信するには、バッファーが小さすぎます。</p>
<p>この値が返された場合、 <strong>InformationToReturn</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーターは、呼び出しに必要なバッファーの最小サイズを設定する必要があります成功します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。 これは、エラー コードです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。 これは、エラー コードです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>クォータはサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxQueryQuotaInfo*受信に応答する[ **IRP\_MJ\_クエリ\_クォータ**](irp-mj-query-quota.md)要求。

呼び出しの前に*MRxQueryQuotaInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryQuota.Length**します。

**QueryQuota.SidList**に設定されているメンバー **IrpSp -&gt;Parameters.QueryQuota.SidList**します。

**QueryQuota.SidListLength**に設定されているメンバー **IrpSp -&gt;Parameters.QueryQuota.SidListLength**します。

**QueryQuota.StartSid**に設定されているメンバー **IrpSp -&gt;Parameters.QueryQuota.StartSid**します。

**QueryQuota.Length**に設定されているメンバー **IrpSp -&gt;Parameters.QueryQuota.Length**します。

**QueryQuota.RestartScan**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_再起動\_スキャン ビットが設定されます。

**QueryQuota.ReturnSingleEntry**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_返す\_単一\_エントリ ビットが設定します。

**QueryQuota.IndexSpecified**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_インデックス\_指定されたビットが設定されます。

成功した場合、ネットワークのミニ リダイレクターを設定する必要があります、 **Info.LengthRemaining** 、RX のメンバー\_返されるクォータ情報の長さのための構造体。 場合に呼び出し*MRxQueryQuotaInfo*が成功した場合は、RDBSS セット、 **IoStatus.Information**に IRP のメンバー、 **Info.LengthRemaining** RXのメンバー\_コンテキスト。

場合に呼び出し*MRxQueryQuotaInfo*は成功しますが、 **InformationToReturn** 、RX のメンバー\_CONTEXT 構造は、返されるクォータ情報の長さを設定する必要があります。 呼び出しが成功した場合、 **InformationToReturn** RX のメンバー\_コンテキストは 0 に設定する必要があります。

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
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

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

 

 






