---
title: フラグ\_Irql ルール (ndis)
description: フラグ\_Irql ルールでは、KeGetCurrentIrql をディスパッチ レベルのフラグ パラメーターが現在の IRQL を示すコールバック関数内で呼び出されませんする必要がありますを指定します。
ms.assetid: 19c5c497-9648-4be9-87d1-82f4fa295351
ms.date: 05/21/2018
keywords:
- Flags_Irql ルール (ndis)
topic_type:
- apiref
api_name:
- Flags_Irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 619c8fab5a7ea6441c80f072632cf661aa3c32e7
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392382"
---
# <a name="flagsirql-rule-ndis"></a>フラグ\_Irql ルール (ndis)


**フラグ\_Irql**ルールを指定する**KeGetCurrentIrql**ディスパッチ レベルのフラグ パラメーターが現在の IRQL を示すコールバック関数の中でないと呼ばれる必要があります。

ディスパッチのレベルのフラグの正しい使用では、IRQL を設定しようと不要なを回避できます。 このフラグを使用する方法の詳細については、次を参照してください。[ディスパッチ IRQL 追跡](https://docs.microsoft.com/windows-hardware/drivers/network/dispatch-irql-tracking)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>Flags_Irql</strong>ルール。</p>
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

 

 





