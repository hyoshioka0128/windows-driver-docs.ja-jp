---
title: WDI タスク コマンドの優先順位と既存の状態
description: アダプターは、特定の状態では、(たとえば、既存の接続に影響を与えるスキャン) の既存の状態に影響を与えることに新しいコマンドがが届く場合があります。
ms.assetid: 11EE42BF-2C44-4601-B262-570E6D154151
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2d485a38cd8f4718ed28bc031ead8ba6a35aa5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356888"
---
# <a name="wdi-task-command-priority-and-existing-state"></a>WDI タスク コマンドの優先順位と既存の状態


アダプターは、特定の状態では、(たとえば、既存の接続に影響を与えるスキャン) の既存の状態に影響を与えることに新しいコマンドがが届く場合があります。 次の表には、新しいコマンドがについて説明します、アダプターでは、既存の状態に対して優先順位を設定する必要があります。 列には、新しいコマンドを受信すると、既存の状態のサービスを提供する方法について説明します。

新しいコマンドの既存状態の接続の品質 (EAP) の優先順位 1 P2P リッスン - 優先順位 2 接続品質の待機時間 (メディア ストリーミング) の優先順位 3 の既存の接続の優先順位 4 スキャン/P2P の検出 (強制) 重要 (遅延スキャン) 一時停止一時停止スロットル スキャン/P2P(非強制) の検出 (スキップ スキャン) の重要重要維持 (スキップ スキャン) スロットル ステーション接続、ローミング、切断遅延接続一時停止一時停止スロットル P2P 移動開始、移動を停止遅延接続一時停止一時停止スロットル P2P クライアント接続、切断遅延接続の一時停止一時停止スロットル P2P 送信アクション応答一時停止一時停止一時停止スロットル P2P 送信アクション要求の遅延送信が一時停止のスロットルを維持します。
 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>重要</p></td>
<td align="left"><p>既存の状態を新しい要求よりも高い優先順位を設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>保守</p></td>
<td align="left"><p>同様に、既存の状態と新しいコマンドを優先します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Throttle</p></td>
<td align="left"><p>動作には、新しいコマンドをより高い優先順位を付けるように、既存の状態のサービスを制限します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>一時停止</p></td>
<td align="left"><p>既存の状態の処理を停止し、既存の状態をできるだけ早く完了しようとしてください。</p></td>
</tr>
</tbody>
</table>

 

 

 





