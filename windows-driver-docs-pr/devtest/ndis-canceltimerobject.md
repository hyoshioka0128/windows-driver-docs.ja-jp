---
title: CancelTimerObject ルール (ndis)
description: CancelTimerObject ルールでは、NdisSetTimerObject と NdisCancelTimerObject が異なる順序でと呼ばれることを指定します。 最終目標は、MiniportHaltEx が終了すると、すべてのタイマーは取り消されるかどうかを確認します。
ms.assetid: F31AF8D2-4F40-43A3-893E-53FCC2299730
ms.date: 05/21/2018
keywords:
- CancelTimerObject ルール (ndis)
topic_type:
- apiref
api_name:
- CancelTimerObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d707717549271db3848f13959f7c303fc77a2f04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570881"
---
# <a name="canceltimerobject-rule-ndis"></a>CancelTimerObject ルール (ndis)


**CancelTimerObject**ルールを指定する[ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)と[ **NdisCancelTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561624)代替の順序で呼び出されます。 最終的な目標はすべてのタイマーが取り消されるかどうかを確認するときに[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が終了します。

ルールは、3 つの異なる状態を使用します。 タイマーが設定または取り消されたときの状態の変更。 タイマーが設定されていつ場合[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)終了すると、ルールは、障害を報告します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CancelTimerObject</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

 

 





