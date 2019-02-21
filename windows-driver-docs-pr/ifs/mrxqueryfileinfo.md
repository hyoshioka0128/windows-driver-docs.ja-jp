---
title: MRxQueryFileInfo routine
description: TheMRxQueryFileInfo ルーチンによって呼び出されます RDBSS を要求できるネットワーク ミニリダイレクター クエリ ファイルの情報をファイル システム オブジェクト。
ms.assetid: 201b749c-527b-4c02-a860-d2f54777dc32
keywords:
- MRxQueryFileInfo ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: e7d7f73472f66c4a8a389a9ebb94a28c02124438
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530563"
---
# <a name="mrxqueryfileinfo-routine"></a>MRxQueryFileInfo routine


*MRxQueryFileInfo*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイル システム オブジェクト上のファイル情報を照会することを要求します。

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

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryFileInfo*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><p>ファイル情報を受け取るバッファーが小さすぎます。</p>
<p>これは戻り値は、成功を考慮してでできるだけの非常に有効なデータとして返す必要がある、 <strong>Info.Buffer</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>要求されたデータを受信するには、バッファーが小さすぎます。</p>
<p>この値が返された場合、 <strong>InformationToReturn</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーターは、呼び出しに必要なバッファーの最小サイズを設定する必要があります成功します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>リモート サーバーから、無効なファイル情報バッファーを受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効なパラメーターが指定されました。</p>
<p>無効な値の場合、この値が返されることができます、 <strong>FileInformationClass</strong> RX_CONTEXT でメンバーが渡されます。 この値は、場合にも返される、 <strong>FileInformationClass</strong>指定されたメンバーが、 <strong>FileStreamInformation</strong>リモート ファイル システムでは、ストリームをサポートしていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>オブジェクト名が見つかりませんでした。 これは、エラー コードです。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

RDBSS への呼び出しを発行する*MRxQueryFileInfo*受信に応答する[ **IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)要求。

呼び出しの前に*MRxQueryFileInfo*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.FileInformationClass**に設定されているメンバー **IrpSp -&gt;Parameters.QueryFile.FileInformationClass**、ファイルを要求された\_情報\_クラス値。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryFile.Length**します。

**QueryDirectory.FileIndex**に設定されているメンバー **IrpSp -&gt;Parameters.QueryDirectory.FileIndex**します。

**QueryDirectory.RestartScan**メンバーが設定される場合**IrpSp -&gt;フラグ**が、SL\_再起動\_スキャン ビットが設定されます。

**QueryDirectory.ReturnSingleEntry**メンバーが設定される場合**IrpSp -&gt;フラグ**が SL\_返す\_単一\_エントリ ビットが設定します。

**QueryDirectory.InitialQuery**メンバーが設定される場合**Fobx -&gt;UnicodeQueryTemplate.Buffer**は**NULL**と**Fobx&gt;フラグ**FOBX を持たない\_フラグ\_一致\_すべてビットが設定されます。

成功した場合、ネットワークのミニ リダイレクターを設定する必要があります、 **Info.LengthRemaining** 、RX のメンバー\_コンテキスト構造体を**Info.Length**ファイル情報の長さマイナス メンバー返されます。 場合に呼び出し*MRxQueryFileInfo*が成功した場合は、RDBSS セット、 **IoStatus.Information**に IRP のメンバー **IrpSp-&gt;Parameters.QueryFile.Length**マイナス、 **Info.LengthRemaining** RX のメンバー\_コンテキスト。

RDBSS は、SL で要求をサポートしていません\_インデックス\_の指定されたビット、 **IrpSp -&gt;フラグ**を設定します。 ネットワークのミニ リダイレクターはへの呼び出しを受信しません*MRxQueryFileInfo* 、SL で\_インデックス\_の指定されたビット**IrpSp -&gt;フラグ**を設定します。

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

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






