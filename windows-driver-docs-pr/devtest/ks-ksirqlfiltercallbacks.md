---
title: KsIrqlFilterCallbacks ルール)
description: KsIrqlFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーがコールバック関数が呼び出された時と同じ IRQL で KS フィルターのコールバック関数から返すことを指定します。
ms.assetid: AC27FF93-DC7C-4287-B3D6-2579FAA65A77
ms.date: 05/21/2018
keywords:
- KsIrqlFilterCallbacks ルール)
topic_type:
- apiref
api_name:
- KsIrqlFilterCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69e38d2c95535a9f8fa934b8526a470798319d6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538295"
---
# <a name="ksirqlfiltercallbacks-rule-"></a>KsIrqlFilterCallbacks ルール)


KsIrqlFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーがコールバック関数が呼び出された時と同じ IRQL で KS フィルターのコールバック関数から返すことを指定します。

**デバッグのヒント**

Driver Verifier は、この規則違反を検出する場合に、トリガー [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)で、 *arg1* 0x00081007 の値。 *Arg3* (RuleState) と*arg4* (下位状態) バグ チェックの規則違反に関する追加情報へのポインターを提供します。

使用して、 [ **! ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374)デバッガーが関数の開始と終了の IRQL の値を確認する拡張機能。

コマンドを使用します。

**! ruleinfo 0x81007** *RuleState* *下位状態*します。

ルールの状態データ、 *OldIrql* IRQL は、コールバックが入力した場合。 *NewIrql* IRQL は、コールバック関数が終了した場合。

使用しない[ **! irql** ](https://msdn.microsoft.com/library/windows/hardware/ff563825) Driver Verifier は、バグ チェックする前に IRQL 発生可能性がありますがなので、現在の IRQL を決定します。 代わりに、 **! verifier 0x008** IRQL を表示するログに記録します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081007) |

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

 

 

 





