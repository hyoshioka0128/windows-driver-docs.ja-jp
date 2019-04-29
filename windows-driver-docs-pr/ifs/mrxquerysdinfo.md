---
title: MRxQuerySdInfo routine
description: TheMRxQuerySdInfo ルーチンによって呼び出されます RDBSS 要求をネットワーク ミニリダイレクター クエリ セキュリティ記述子の情報をファイル システム オブジェクト。
ms.assetid: 5bab05f1-2a79-42c0-ba70-e1124f7b1528
keywords:
- MRxQuerySdInfo ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 072590cdf56942140b974362c1b3ec13928a5128
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324262"
---
# <a name="mrxquerysdinfo-routine"></a>MRxQuerySdInfo routine


*MRxQuerySdInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクトのセキュリティ記述子の情報を照会することを要求します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQuerySdInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><p>セキュリティ記述子の情報を受信するバッファーが小さすぎます。</p>
<p>これは戻り値は、成功を考慮してでできるだけの非常に有効なデータとして返す必要がある、 <strong>Info.Buffer</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>要求されたデータを受信するには、バッファーが小さすぎます。</p>
<p>この値が返された場合、 <strong>InformationToReturn</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーターは、呼び出しに必要なバッファーの最小サイズを設定する必要があります成功します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>接続が切断されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワーク アクセスが拒否されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>リモートのページ ファイルに関する情報など、要求された機能が実装されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>セキュリティ記述子の情報は、リモート共有に対するサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクトのパスが見つかりませんでした。 このエラーは、NTFS ストリーム オブジェクトの情報を要求したし、リモート ファイル システムがストリームをサポートしていない場合に返されることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>シンボリック リンクを処理するために、再解析が必要です。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxQuerySdInfo*受信に応答する[ **IRP\_MJ\_クエリ\_セキュリティ**](irp-mj-query-security.md)要求。

呼び出しの前に*MRxQuerySdInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**QuerySecurity.SecurityInformation**に設定されているメンバー **IrpSp -&gt;Parameters.QuerySecurity.SecurityInformation**します。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QuerySecurity.Length**します。

成功した場合、ネットワークのミニ リダイレクターを設定する必要があります、 **InformationToReturn** 、RX のメンバー\_セキュリティ情報の長さの CONTEXT 構造体が返されます。 場合に呼び出し*MRxQuerySdInfo*が成功した場合は、RDBSS セット、 **IoStatus.Information**に IRP のメンバー、 **InformationToReturn** RX のメンバー\_コンテキスト。

<a name="requirements"></a>必要条件
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

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






