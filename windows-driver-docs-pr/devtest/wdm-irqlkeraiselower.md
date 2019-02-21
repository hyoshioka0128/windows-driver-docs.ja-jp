---
title: IrqlKeRaiseLower ルール (wdm)
description: IrqlKeRaiseLower ルールでは、IRQL とドライバー値の増減 KeRaiseIrql を呼び出すときに、ドライバーは次の処理、NewIrql パラメーターの値以下である IRQL で実行されていることを指定します。ドライバーは、KeRaiseIrql または KeRaiseIrqlToDpcLevel を呼び出した後にだけ KeLowerIrql を呼び出します。
ms.assetid: 61f7e5bc-ccc5-4ee6-a580-9935a01f96e6
ms.date: 05/21/2018
keywords:
- IrqlKeRaiseLower ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeRaiseLower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca77b426cdf58c0c34ec7c818e43094fa0ea0e15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535676"
---
# <a name="irqlkeraiselower-rule-wdm"></a>IrqlKeRaiseLower ルール (wdm)


**IrqlKeRaiseLower**ルールでは、ドライバーは、IRQL 値の増減すると、次でことを指定します。

ドライバーを呼び出すと[ **KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079)よりも小さい IRQL で実行されているかの値と等しく、 *NewIrql*パラメーター。
ドライバー呼び出し[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)呼び出した後のみ**KeRaiseIrql**または[ **KeRaiseIrqlToDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553084).
このルールにより、入れ子になった呼び出し**KeRaiseIrql**、 **KeRaiseIrqlToDpcLevel**、および**KeLowerIrql**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeRaiseLower</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)
[**KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)も参照してください
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md)
[**IrqlKeRaiseLower2**](wdm-irqlkeraiselower2.md)
 

 





