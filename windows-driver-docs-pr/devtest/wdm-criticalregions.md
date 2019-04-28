---
title: CriticalRegions ルール (wdm)
description: CriticalRegions ルールは、ドライバーが KeLeaveCriticalRegion を呼び出す前に KeEnterCriticalRegion を呼び出す必要があります、KeEnterCriticalRegion への後続の呼び出しの前に、ドライバーが KeLeaveCriticalRegion を呼び出すことを指定します。 (入れ子になった呼び出しが許可されます。)。
ms.assetid: 5976e24b-ca1c-440e-97c8-ccc2015d1172
ms.date: 05/21/2018
keywords:
- CriticalRegions ルール (wdm)
topic_type:
- apiref
api_name:
- CriticalRegions
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 229bfc4462f7e32aa781b207b947e37986328ed6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363492"
---
# <a name="criticalregions-rule-wdm"></a>CriticalRegions ルール (wdm)


**CriticalRegions**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)呼び出す前に[ **KeLeaveCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552964)ドライバーを呼び出すと**KeLeaveCriticalRegion**への後続の呼び出しの前に**KeEnterCriticalRegion**します。 (入れ子になった呼び出しが許可されます。)

このルールは、ドライバーを呼び出すことを指定しますも**KeLeaveCriticalRegion**を返す前に、通常のカーネルの非同期プロシージャ コール (Apc) の配信を再度有効にします。

WDK ドキュメントの**KeEnterCriticalRegion**と**KeLeaveCriticalRegion** IRQL でこれらの関数の呼び出し元を実行できることについて説明します。&lt;APC を =\_レベル。 このような状況では、このルールは、ベスト プラクティスの推奨事項を適用します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00040003) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CriticalRegions</strong>ルール。</p>
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208#ddi-compliance-checking-additional" data-raw-source="[DDI compliance checking (additional)](https://msdn.microsoft.com/library/windows/hardware/hh454208#ddi-compliance-checking-additional)">DDI 準拠の確認 (追加)</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**ExEnterCriticalRegionAndAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/dn308550)
[**ExReleaseResourceAndLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/dn308551)
[**KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)
[**KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)
 

 





