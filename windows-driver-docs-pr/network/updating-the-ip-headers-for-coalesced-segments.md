---
title: まとめられたセグメントの IP ヘッダーを更新しています
description: このセクションは、まとめられたセグメントの IP ヘッダーを更新する方法を説明します
ms.assetid: 18F2944A-D5A7-41BB-885F-EC183A00F7CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e99f33d7e13c78941b68d898866827f653a6a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340922"
---
# <a name="updating-the-ip-headers-for-coalesced-segments"></a>結合されたセグメントの IP ヘッダーの更新


1 つの結合単位 (SCU) の最終処理中、ときに、受信セグメントの合体 (RSC)-対応ミニポート ドライバーは、次の表で説明したように IP ヘッダーのフィールドを更新します。

-   [まとめられたセグメントの IPv4 ヘッダー フィールドを更新しています](#updating-ipv4-header-fields-for-coalesced-segments)
-   [まとめられたセグメントの IPv6 ヘッダー フィールドを更新しています](#updating-ipv6-header-fields-for-coalesced-segments)

## <a name="updating-ipv4-header-fields-for-coalesced-segments"></a>まとめられたセグメントの IPv4 ヘッダー フィールドを更新しています


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>バージョン</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ヘッダーの長さ</strong></p></td>
<td align="left"><p>IP オプションを指定せずに基本的な IPv4 ヘッダーの長さ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>差別化されたサービス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ECN ビット</strong></p></td>
<td align="left"><p>8 での例外を参照してください。<a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">例外条件の結合の終了を</a>します。 ECN ビットの値が同じであるすべての場合、データグラムを結合する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>長さの合計</strong></p></td>
<td align="left"><p>このフィールドの値は、既存の SCU に TCP ペイロード長が 0 以外の新しいセグメントを統合するたびに再計算する必要があります。 参照してください<a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">例外条件がその終了結合</a>のこのフィールドの値に起因する特殊なケースです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Identification</strong></p></td>
<td align="left"><p>最初の結合されたセグメントの IP の ID に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>フラグ</strong></p></td>
<td align="left"><ul>
<li><p>データグラムは、DF (断片化しない) のビットの値が同じである限り、結合された可能性があります。 すべてのセット、またはすべてクリアします。</p></li>
<li><p>MF (複数のフラグメント) ビットが設定されたセグメントを結合していない必要があります。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>フラグメントのオフセット</strong></p></td>
<td align="left"><p>適用できません。 IP データグラムの断片化をひとまとめにありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Time To Live</strong></p></td>
<td align="left"><p>有効なまとめられたセグメントの (有効期間 TTL) 値を時間の最小値に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>[プロトコル]</strong></p></td>
<td align="left"><p>常に TCP を 6 に設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ヘッダーのチェックサム</strong></p></td>
<td align="left"><p>このフィールドの値は、ミニポート ドライバーによって再計算する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>送信元アドレス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>送信先アドレス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="updating-ipv6-header-fields-for-coalesced-segments"></a>まとめられたセグメントの IPv6 ヘッダー フィールドを更新しています


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>バージョン</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>トラフィック クラス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>フローのラベル</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ペイロードの長さ</strong></p></td>
<td align="left"><p>このフィールドの値は、既存のセグメントに TCP ペイロード長が 0 以外の場合、新しいセグメントが統合されるたびに再計算する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>次のヘッダー</strong></p></td>
<td align="left"><p>常に TCP を 6 に設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ホップの制限</strong></p></td>
<td align="left"><p>最小値に設定する必要があります<strong>ホップ制限</strong>まとめられたセグメントの値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>送信元アドレス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>送信先アドレス</strong></p></td>
<td align="left"><p>このフィールドの値は、すべての結合されたセグメントに対して同じである必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





