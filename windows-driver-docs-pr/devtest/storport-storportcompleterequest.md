---
title: StorPortCompleteRequest ルール (storport)
description: このルールは、ミニポートによって StorPortCompleteRequest への呼び出しが行われていないことを確認します。 StorPortCompleteRequest の使用は推奨されません。ミニポートは、notificationType RequestComplete で StorPortNotification を代わりに呼び出す必要があります。
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
ms.openlocfilehash: bdeb999c6ef1fd2760fa0e07c77bd62e1259c9f6
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391852"
---
# <a name="storportcompleterequest-rule-storport"></a>StorPortCompleteRequest ルール (storport)


このルールを確認するを呼び出せなく**StorPortCompleteRequest**ミニポートによって行われます。 使用状況、 **StorPortCompleteRequest**は推奨されません。 ミニポートが代わりに呼び出す必要があります**StorPortNotification**で**notificationType = RequestComplete**します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortCompleteRequest</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**StorPortCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportcompleterequest)
 

 





