---
title: IrqlKeRaiseLower2 ルール (wdm)
description: IrqlKeRaiseLower2 ルールは、ドライバーが Ke Irql を使用して、以前の KeRaiseIrql または KeRaiseIrqlToDpcLevel の呼び出しによって発生した元の IRQL を復元するように指定します。
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
ms.openlocfilehash: b4bd3356d203d2219cfff882c8189fa8146b3ee3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917890"
---
# <a name="irqlkeraiselower2-rule-wdm"></a>IrqlKeRaiseLower2 ルール (wdm)


**IrqlKeRaiseLower2**ルールは、ドライバーが[**ke irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)を使用して、以前の[**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)または[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)の呼び出しによって発生した元の irql を復元するように指定します。

このルールは、 **Keraiseirql**、 **KeRaiseIrqlToDpcLevel** 、および**kelowerirql**の入れ子になった呼び出しを許可します。

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlKeRaiseLower2</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**Ke-irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) 
[**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)関連項目
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md) 
[ **Irqlkeraiselower**](wdm-irqlkeraiselower.md)
 

 





