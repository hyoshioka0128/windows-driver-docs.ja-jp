---
title: IrqlReturn ルール (wdm)
description: IrqlReturn ルールでは、ドライバーのディスパッチルーチンが、呼び出されたときと同じ IRQL で返されることを指定します。
ms.assetid: 1b2ef432-e3ba-4a01-b3df-839ff13b03f6
ms.date: 05/21/2018
keywords:
- IrqlReturn ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6714b3994f5a6b56e62a3941d5fd337547961372
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917814"
---
# <a name="irqlreturn-rule-wdm"></a>IrqlReturn ルール (wdm)


**Irqlreturn**ルールでは、ドライバーのディスパッチルーチンが、呼び出されたときと同じ IRQL で返されることを指定します。 ディスパッチルーチンが適切に呼び出される IRQLs の詳細については、「 [**ディスパッチルーチンと IRQLs** 」を参照してください。](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls)

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>irqlreturn</strong>ルールを指定します。</p>
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

<a name="see-also"></a>こちらもご覧ください
--------

[**ディスパッチ ルーチンと IRQL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls)
 

 





