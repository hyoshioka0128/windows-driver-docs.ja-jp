---
title: MRxQueryDirectory ルーチン
description: MRxQueryDirectory ルーチンによって呼び出されますを要求できる RDBSS ネットワーク ミニリダイレクター クエリについては、ファイルのディレクトリで。
ms.assetid: 26c7c7fa-7dfa-43fb-a1db-cfc2fc40b969
keywords:
- MRxQueryDirectory ルーチン インストール可能なファイル システム ドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryDirectory
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4d3d93833fc553b4a2e98f2fcc3e1129ba7214
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581790"
---
# <a name="mrxquerydirectory-routine"></a>MRxQueryDirectory ルーチン


*MRxQueryDirectory*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニ リダイレクターがファイルのディレクトリの情報を照会することを要求します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryDirectory;

NTSTATUS MRxQueryDirectory(
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

*MRxQueryDirectory*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリ完了までのリソースの不足が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>リモート サーバーから、無効なファイル情報バッファーを受け取りましたまたは返されたファイル名の長さが許容最大長を超えています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>無効な FileInformationClass がで指定された、 <strong>Info.FileInformationClass</strong>によって示される RX_CONTEXT 構造体のメンバー、 <em>RxContext</em>パラメーター。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>クエリ完了までのリモート サーバーへの再接続に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NO_SUCH_FILE</strong></td>
<td align="left"><p>すべてのエントリを検索するクエリが失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>共有違反が発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

呼び出しの前に*MRxQueryDirectory*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**Info.FileInformationClass**に設定されているメンバー **IrpSp -&gt;Parameters.QueryDirectory.FileInformationClass**します。

**Info.Buffer**メンバーは、I/O 要求パケットからユーザー バッファーに設定されます。 このバッファーが RDBSS によってロックされて既に必要な場合。

**Info.LengthRemaining**に設定されているメンバー **IrpSp -&gt;Parameters.QueryDirectory.Length**します。

**QueryDirectory.FileIndex**に設定されているメンバー **IrpSp -&gt;Parameters.QueryDirectory.FileIndex**します。

**QueryDirectory.RestartScan**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_再起動\_ビットをスキャンします。

**QueryDirectory.ReturnSingleEntry**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_返す\_単一\_ビットにエントリ。

**QueryDirectory.IndexSpecified**メンバーが 0 以外の値に設定されている**IrpSp -&gt;フラグ**が、SL\_インデックス\_ビットを指定します。

**QueryDirectory.InitialQuery**メンバーが 0 以外の値に設定されている**UnicodeQueryTemplate.Buffer**関連付けられている FOBX のメンバーが**NULL**と**フラグ** FOBX のメンバーには、FOBX はありません。\_フラグ\_一致\_ですべてのビット。

ワイルドカード クエリ ("\*.\*"など)、RDBSS は設定、 **UnicodeQueryTemplate.Buffer**ワイルドカード クエリに関連付けられている FOBX のメンバーが渡されます。

場合、 **PostRequest** 、RX のメンバー\_CONTEXT 構造は**TRUE**戻り時にから*MRxQueryDirectory*、RDBSS は呼び出す[ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472) RX を渡す\_ワーカー キュー、ファイル システムのプロセス (FSP) による処理のための構造体。

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

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

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

[**RxFsdPostRequest**](https://msdn.microsoft.com/library/windows/hardware/ff554472)

 

 





