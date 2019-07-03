---
title: バグ チェック 0x15F CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
description: CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP のバグ チェックでは、0x0000015F の値を持ちます。 これは、コネクテッド スタンバイ ウォッチドッグ タイムアウトが発生したことを示します。
ms.assetid: 4C10AAC1-0B8F-4BBE-B470-55A8ED373687
keywords:
- バグ チェック 0x15F CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
- CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9901d8484f06e9dda095b5446098682c990ba45c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519997"
---
# <a name="bug-check-0x15f-connectedstandbywatchdogtimeoutlivedump"></a>バグ チェック 0x15F:接続されている\_スタンバイ\_ウォッチドッグ\_タイムアウト\_LIVEDUMP


接続済み、\_スタンバイ\_ウォッチドッグ\_タイムアウト\_LIVEDUMP バグ チェックが 0x0000015F の値を持ちます。 これは、コネクテッド スタンバイ ウォッチドッグ タイムアウトが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="connectedstandbywatchdogtimeoutlivedump-parameters"></a>接続されている\_スタンバイ\_ウォッチドッグ\_タイムアウト\_LIVEDUMP パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>CS ウォッチドッグ サブコード</p>
0x1:DRIPS ウォッチドッグがタイムアウトしました。 システムは、DRIPS (最下位ランタイム プラットフォームのアイドル状態) を入力しなくても時間が長すぎる、コネクト スタンバイありませんアクティベーターがアクティブとデバイスの制限はなくの未指定の回復性の段階で導入されました。
<p>2 - 追加情報 (nt へのポインター!POP_DRIPS_WATCHDOG_METRICS)</p>
<p>3-非-DRIPS 時間 (ミリ秒)</p>
<p>4-予約されています</p>
0x2:DRIPS はウォッチドッグ デバイス制約のタイムアウトです。 システムは、ありませんアクティベーターがアクティブで、未指定のデバイスの制約により DRIPS (最下位ランタイム プラットフォームのアイドル状態) を入力せずには、時間が長すぎるのコネクト スタンバイの回復性の段階で導入されました。
<p>2-nt!TRIAGE_POP_FX_DEVICE デバイス</p>
<p>3-コンポーネント インデックス</p>
<p>4-予約されています</p>
0x3:DRIPS はウォッチドッグ preveto タイムアウトです。 システムは、DRIPS (最下位ランタイム プラットフォームのアイドル状態) を入力するため、アクティブな PEP 前拒否未指定のデバイスの制約がないとありませんアクティベーターがアクティブな時間が長すぎるせず、コネクト スタンバイの回復性のフェーズで導入されました。
<p>2-拒否コード</p>
<p>3 - 拒否名の文字列 (PWSTR) へのポインター</p>
<p>4-PEP PPM コールバックへのポインター</p>
0x4:ディープ スリープ ウォッチドッグ
<p>2-メトリック</p>
<p>3 -NonDeepSleepDurationMs</p>
<p>4-予約されています</p>
0x5。ディープ スリープ電源設定のウォッチドッグ
<p>2-メトリック</p>
<p>3 -NonDeepSleepDurationMs</p>
<p>4-予約されています</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">パラメーター 1 を参照してください。</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このマシンには、画面オフ バッテリの寿命を削減する動作が発生しています。 通常これは、CPU アクティビティ、デバイスのアクティビティ、またはデバイスが不足しているアイドル状態になることが原因です。

 

 




