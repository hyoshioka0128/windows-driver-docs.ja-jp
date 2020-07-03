---
title: PagedCodeAtPowerTrans ルール (wdm)
description: PagedCodeAtPowerTrans ルールでは、システムの IRP MJ 電源 Irp (IRP) に応答しているときに、ドライバーがページングされたコードを呼び出さないように指定し \_ \_ \_ \_ \_ \_ ます。また、デバイスの irp \_ MJ \_ 電源 (irp) に応答し \_ \_ \_ ます。
ms.assetid: D94B0E13-9640-4FBF-B1E7-AF8DFED42542
ms.date: 05/21/2018
keywords:
- PagedCodeAtPowerTrans ルール (wdm)
topic_type:
- apiref
api_name:
- PagedCodeAtPowerTrans
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8f7c991d0f730f5a19ec03394a062079eca39d98
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917702"
---
# <a name="pagedcodeatpowertrans-rule-wdm"></a>PagedCodeAtPowerTrans ルール (wdm)


**PagedCodeAtPowerTrans**ルールでは、システムの irp MJ 電源 IRP (irp) に応答しているときに、ドライバーがページングされた[** \_ コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出さないように指定し \_ \_ \_ \_ \_ ます。また、デバイスの irp \_ MJ \_ 電源 (irp) に応答し \_ \_ \_ ます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>PagedCodeAtPowerTrans</strong>規則を指定します。</p>
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

[**ページング \_ コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
 

 





