---
title: MRxQueryDirectory ルーチン
description: MRxQueryDirectory ルーチンは RDBSS によって呼び出され、ネットワークミニリダイレクターがファイルディレクトリに関する情報を照会するように要求します。
ms.assetid: 26c7c7fa-7dfa-43fb-a1db-cfc2fc40b969
keywords:
- MRxQueryDirectory ルーチンのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: ef35dd5a37265c13b45a73a6c6964064d87216ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841092"
---
# <a name="mrxquerydirectory-routine"></a>MRxQueryDirectory ルーチン


*MRxQueryDirectory*ルーチンは[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出され、ネットワークミニリダイレクターがファイルディレクトリに関する情報を照会するように要求します。

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

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxQueryDirectory*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>クエリを完了するためのリソースが不足しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>リモートサーバーから無効なファイル情報バッファーを受信したか、返されたファイル名の長さが許容最大長を超えました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>RxContext パラメーターによって示されている RX_CONTEXT 構造体の <strong>クラス</strong>メンバーに無効な fileinformationclass が指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>リモートサーバーに再接続してクエリを完了できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NO_SUCH_FILE</strong></td>
<td align="left"><p>クエリでエントリが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>共有違反が発生しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxQueryDirectory*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**Info. fileinformationclass**メンバーは**irpsp-&gt;Parameters. Querydirectory. fileinformationclass**に設定されます。

**情報バッファー**のメンバーは、i/o 要求パケットからのユーザーバッファーに設定されます。 このバッファーは、必要に応じて、RDBSS によって既にロックされています。

**LengthRemaining**メンバーは**irpsp-&gt;Parameters. Querydirectory. Length**に設定されています。

**Querydirectory. fileindex**メンバーは**irpsp-&gt;Parameters. Querydirectory. fileindex**に設定されます。

**Irpsp-&gt;フラグ**に SL\_再起動\_スキャンビットがある場合、 **RestartScan**メンバーは0以外に設定されます。

**Irpsp-&gt;フラグ**に SL\_\_単一\_エントリビットが返される場合、**このメンバーは0以外の値**に設定されます。

**Irpsp-&gt;フラグ**に SL\_インデックス\_指定されたビットがオンになっている場合、**指定さ**れたメンバーは0以外に設定されます。

関連する FOBX の**UnicodeQueryTemplate**メンバーが NULL で、Fobx の**Flags**メンバーが fobx\_フラグ\_一致しない場合、 **querydirectory. initialquery**メンバーは0以外の**値**に設定され\_ALL bit on。

ワイルドカードクエリ ("\*。\*"など) の場合、RDBSS は、関連付けられている FOBX の**UnicodeQueryTemplate**メンバーを、渡されたワイルドカードクエリに設定します。

*MRxQueryDirectory*から返されたときに RX\_コンテキスト構造の**Postrequest**メンバーが**TRUE**の場合、RDBSS は[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)を呼び出して、によって処理するために rx\_コンテキスト構造をワーカーキューに渡します。ファイルシステムプロセス (FSP)。

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

[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)

 

 






