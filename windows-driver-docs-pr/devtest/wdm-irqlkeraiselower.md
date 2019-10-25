---
title: IrqlKeRaiseLower ルール (wdm)
description: IrqlKeRaiseLower ルールでは、ドライバーが KeRaiseIrql を呼び出したときに IRQL を上げたり下げたりするときに、ドライバーが次のことを行うことを指定します。これは、NewIrql パラメーターの値以下の IRQL で実行されています。ドライバーは、KeRaiseIrql または KeRaiseIrqlToDpcLevel を呼び出した後にのみ KeLowerIrql を呼び出します。
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
ms.openlocfilehash: 0aea4556183eb4820a6885fdad6bd41d9c459624
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839179"
---
# <a name="irqlkeraiselower-rule-wdm"></a>IrqlKeRaiseLower ルール (wdm)


**Irqlkeraiselower**ルールでは、IRQL を上げたり下げたりするときに、ドライバーが次のことを実行することを指定します。

ドライバーが[**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)を呼び出すと、 *NewIrql*パラメーターの値以下の irql で実行されます。
ドライバーは、 **Keraiseirql**または[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)を呼び出した後にのみ[**kelowerirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)を呼び出します。
このルールは、 **Keraiseirql**、 **KeRaiseIrqlToDpcLevel**、および**kelowerirql**の入れ子になった呼び出しを許可します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irqlkeraiseselower</strong>ルールを指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**Ke+ irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)
[**keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)に関する参照
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md)
[ **IrqlKeRaiseLower2**](wdm-irqlkeraiselower2.md)
 

 





