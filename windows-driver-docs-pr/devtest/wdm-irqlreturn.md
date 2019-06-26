---
title: IrqlReturn ルール (wdm)
description: IrqlReturn ルールでは、ドライバーのディスパッチ ルーチンが呼び出される位置同じ IRQL で返すことを指定します。
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
ms.openlocfilehash: d9a7f5eba63151d34cc7be283c505369f41c7f5d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392062"
---
# <a name="irqlreturn-rule-wdm"></a>IrqlReturn ルール (wdm)


**IrqlReturn**ルールでは、ドライバーのディスパッチ ルーチンが呼び出される位置同じ IRQL で返すことを指定します。 ルーチンは正しくするディスパッチで呼び出される Irql の詳細については、次を参照してください。 [**ディスパッチ ルーチンは、Irql します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls)

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>IrqlReturn</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>関連項目
--------

[**ディスパッチ ルーチンは、Irql**](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls)
 

 





