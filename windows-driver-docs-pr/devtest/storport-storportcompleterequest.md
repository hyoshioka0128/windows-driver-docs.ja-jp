---
title: StorPortCompleteRequest ルール (storport)
description: このルールは、StorPortCompleteRequest への呼び出しがミニポートによって行われていないことを確認します。 StorPortCompleteRequest の使用は推奨されません。ミニポートは、代わりに notificationType RequestComplete で StorPortNotification を呼び出す必要があります。
ms.assetid: 6DDAC83F-C4D5-4600-B5F3-AA7F216BB797
ms.date: 05/21/2018
keywords:
- StorPortCompleteRequest ルール (storport)
topic_type:
- apiref
api_name:
- StorPortCompleteRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a510d90ae63dee06a2c5dd87a6d969b38de9c767
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839288"
---
# <a name="storportcompleterequest-rule-storport"></a>StorPortCompleteRequest ルール (storport)


このルールは、 **StorPortCompleteRequest**への呼び出しがミニポートによって行われていないことを確認します。 **StorPortCompleteRequest**の使用は推奨されません。ミニポートは、代わりに**notificationType = RequestComplete**で**storportnotification**を呼び出す必要があります。

|              |          |
|--------------|----------|
| ドライバーモデル | Storport |

<a name="how-to-test"></a>テストする方法
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>StorPortCompleteRequest</strong>規則を指定します。</p>
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

[**StorPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportcompleterequest)
 

 





