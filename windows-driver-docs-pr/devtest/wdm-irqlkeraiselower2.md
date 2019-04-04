---
title: IrqlKeRaiseLower2 ルール (wdm)
description: IrqlKeRaiseLower2 ルールでは、ドライバーが KeRaiseIrql または KeRaiseIrqlToDpcLevel 前の呼び出しによって発生した元の IRQL を復元する KeLowerIrql を使用することを指定します。
ms.assetid: 7e256237-e649-45de-bcd9-b06795a5c5c9
ms.date: 05/21/2018
keywords:
- IrqlKeRaiseLower2 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeRaiseLower2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbf7c19bd175b05f8cb09527ea7524c2dca7cd27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574842"
---
# <a name="irqlkeraiselower2-rule-wdm"></a>IrqlKeRaiseLower2 ルール (wdm)


**IrqlKeRaiseLower2**ルールでは、ドライバーが使用することを指定します[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)前の呼び出しによって発生した元の IRQL を復元する[ **KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)または[ **KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)します。

このルールにより、入れ子になった呼び出し**KeRaiseIrql**、 **KeRaiseIrqlToDpcLevel**と**KeLowerIrql**します。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeRaiseLower2</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)
[**KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)も参照してください
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md)
[**IrqlKeRaiseLower**](wdm-irqlkeraiselower.md)
 

 





