---
title: MRxQueryEaInfo ルーチン
description: MRxQueryEaInfo ルーチンは、ネットワークのミニ リダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求する RDBSS によって呼び出されます。
ms.assetid: 4471eb82-c176-4976-b722-5a6e067a7e69
keywords:
- MRxQueryEaInfo ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: e52733bd8cde2037a4395b03d963a0c3c64948ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324346"
---
# <a name="mrxqueryeainfo-routine"></a>MRxQueryEaInfo ルーチン


*MRxQueryEaInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニリダイレクター クエリがファイル システム オブジェクトの属性情報を拡張することを要求します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryEaInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><p>拡張属性の情報を受け取るバッファーが小さすぎます。</p>
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
<td align="left"><strong>STATUS_EA_CORRUPT_ERROR</strong></td>
<td align="left"><p>拡張属性の無効な情報は、リモート サーバーから受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NONEXISTENT_EA_ENTRY</strong></td>
<td align="left"><p>ファイル オブジェクトの拡張属性がないと、ユーザーは、拡張属性のインデックスを提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>拡張属性はサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>SRV_OPEN 構造が接続されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REQUEST_ABORTED</strong></td>
<td align="left"><p>ネットワーク要求が中止されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxQueryEaInfo*受信に応答する[ **IRP\_MJ\_クエリ\_EA** ](irp-mj-query-ea.md)要求。

呼び出しの前に*MRxQueryEaInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryEa.Length**します。

**QueryEa.UserEaList**に設定されているメンバー **IrpSp -&gt;Parameters.QueryEa.EaList**します。

**QueryEa.UserEaListLength**に設定されているメンバー **IrpSp -&gt;Parameters.QueryEa.EaListLength**します。

**QueryEa.UserEaIndex**に設定されているメンバー **IrpSp -&gt;Parameters.QueryEa.EaIndex**します。

**QueryEa.RestartScan**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_再起動\_ビットをスキャンします。

**QueryEa.ReturnSingleEntry**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_返す\_単一\_ビットにエントリ。

**QueryEa.IndexSpecified**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_インデックス\_ビットを指定します。

成功した場合、 *MRxQueryEaInfo*設定する必要があります、 **Info.LengthRemaininging** 、RX のメンバー\_コンテキスト構造体は、返される拡張属性の情報も更新プログラムの長さを**Fobx -&gt;OffsetOfNextEaToReturn**メンバー。 場合に呼び出し*MRxQueryEaInfo*が成功した場合は、RDBSS セット、 **IoStatus.Information**に IRP のメンバー **IrpSp -&gt;Parameters.QueryEa.Length**マイナス、 **Info.LengthRemaining** RX のメンバー\_コンテキスト。

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

 

 






