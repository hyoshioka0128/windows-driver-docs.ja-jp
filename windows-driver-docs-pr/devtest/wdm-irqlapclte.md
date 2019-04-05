---
title: IrqlApcLte ルール (wdm)
description: IrqlApcLte ルールでは、IRQL APC で実行されている場合にのみに、ドライバーで ObGetObjectSecurity と ObReleaseObjectSecurity を呼び出すことを指定します\_レベル。
ms.assetid: 83f18eb3-aee1-403e-90a2-c03b81109ebb
ms.date: 05/21/2018
keywords:
- IrqlApcLte ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc12e5ef1623d425fd16ea9043dd6da57cace7b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553808"
---
# <a name="irqlapclte-rule-wdm"></a>IrqlApcLte ルール (wdm)


**IrqlApcLte**ルールでは、ドライバーを呼び出すことを指定します[ **ObGetObjectSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff557738)と[ **ObReleaseObjectSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff558695) IRQL でその実行はときにのみ&lt;APC を =\_レベル。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**0 xa-チェックをバグします。IRQL\_いない\_少ない\_または\_等しい**](https://msdn.microsoft.com/library/windows/hardware/ff560129)、 [**チェック 0xC4 のバグします。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020002) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlApcLte</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
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

 

<a name="applies-to"></a>適用対象
----------

[**ObGetObjectSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff557738)
[**ObReleaseObjectSecurity** ](https://msdn.microsoft.com/library/windows/hardware/ff558695)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





