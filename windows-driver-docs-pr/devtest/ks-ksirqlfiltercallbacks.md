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
ms.openlocfilehash: 828d254907e8f6ce15fb80622d0e97b189c60a03
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392754"
---
# <a name="ksirqlfiltercallbacks-rule-"></a>KsIrqlFilterCallbacks ルール)


KsIrqlFilterCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーがコールバック関数が呼び出された時と同じ IRQL で KS フィルターのコールバック関数から返すことを指定します。

**デバッグのヒント**

Driver Verifier は、この規則違反を検出する場合に、トリガー [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)で、 *arg1* 0x00081007 の値。 *Arg3* (RuleState) と*arg4* (下位状態) バグ チェックの規則違反に関する追加情報へのポインターを提供します。

使用して、 [ **! ruleinfo** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo)デバッガーが関数の開始と終了の IRQL の値を確認する拡張機能。

コマンドを使用します。

**! ruleinfo 0x81007** *RuleState* *下位状態*します。

ルールの状態データ、 *OldIrql* IRQL は、コールバックが入力した場合。 *NewIrql* IRQL は、コールバック関数が終了した場合。

使用しない[ **! irql** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-irql) Driver Verifier は、バグ チェックする前に IRQL 発生可能性がありますがなので、現在の IRQL を決定します。 代わりに、 **! verifier 0x008** IRQL を表示するログに記録します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00081007) |

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
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





