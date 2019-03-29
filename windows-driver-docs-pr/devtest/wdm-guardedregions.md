---
title: GuardedRegions ルール (wdm)
description: GuardedRegions ルールは、厳密な交互に KeEnterGuardedRegion および KeLeaveGuardedRegion への呼び出しが使用されることを確認します。
ms.assetid: CF98BF68-905C-48D2-AE72-08DD5559AA0D
ms.date: 05/21/2018
keywords:
- GuardedRegions ルール (wdm)
topic_type:
- apiref
api_name:
- GuardedRegions
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af9be3cd3fd0f95460d53adc736c09abaa99b532
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577650"
---
# <a name="guardedregions-rule-wdm"></a>GuardedRegions ルール (wdm)


**GuardedRegions**への呼び出し規則を確認します[ **KeEnterGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552028)と[ **KeLeaveGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552967)厳密な代替構成で使用されます。

呼び出しごとに[ **KeEnterGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552028)に一致する呼び出しがあります。 [ **KeLeaveGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552967)します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0004000E) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>GuardedRegions</strong>ルール。</p>
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**KeEnterGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552028)
[**KeLeaveGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552967)も参照してください
--------

[重要な領域と保護された領域](https://msdn.microsoft.com/library/windows/hardware/ff542925)
 

 





