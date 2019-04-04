---
title: KsIrqlPinCallbacks rule ()
description: KsIrqlPinCallbacks ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが呼び出された時と同じ IRQL で KS Pin コールバック関数から返すことを指定します。
ms.assetid: B2C1413A-9B94-499A-A15C-A943065F7CA1
ms.date: 05/21/2018
keywords:
- KsIrqlPinCallbacks rule ()
topic_type:
- apiref
api_name:
- KsIrqlPinCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 736561ace3e352a3467fef9176c81a89a820b719
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537702"
---
# <a name="ksirqlpincallbacks-rule-"></a>KsIrqlPinCallbacks rule ()


KsIrqlPinCallbacks ルールでは、カーネル ストリーム (KS) ミニポート ドライバーが呼び出された時と同じ IRQL で KS Pin コールバック関数から返すことを指定します。

**デバッグのヒント**

Driver Verifier は、この規則違反を検出する場合に、トリガー [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)で、 *arg1* 0x00081008 の値。 *Arg3* (RuleState) と*arg4* (下位状態) バグ チェックの規則違反に関する追加情報へのポインターを提供します。

使用して、 [ **! ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)デバッガーが関数の開始と終了の IRQL の値を確認する拡張機能。

コマンドを使用します。

**! ruleinfo 0x81008** *RuleState* *下位状態*します。

ルールの状態データ、 *OldIrql* IRQL は、コールバックが入力した場合。 *NewIrql* IRQL は、コールバック関数が終了した場合。

使用しない[ **! irql** ](https://msdn.microsoft.com/library/windows/hardware/ff563825) Driver Verifier は、バグ チェックする前に IRQL 発生可能性がありますがなので、現在の IRQL を決定します。 代わりに、 **! verifier 0x008** IRQL を表示するログに記録します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081008) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain ks</strong>します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





