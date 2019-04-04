---
title: EvtSurpriseRemoveNoRequestComplete ルール (kmdf)
description: EvtSurpriseRemoveNoRequestComplete ルールでは、ドライバーを WDF EvtDeviceSurpriseRemoval コールバックからの要求を完了しないでください、代わりに、自己管理型の I/O のコールバック関数を使用することを指定します。
ms.assetid: A815CFA0-72A9-4FBC-8432-6212CB696F99
ms.date: 05/21/2018
keywords:
- EvtSurpriseRemoveNoRequestComplete ルール (kmdf)
topic_type:
- apiref
api_name:
- EvtSurpriseRemoveNoRequestComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c90876debc6cd2beddd244e6373015d796b8ed2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551389"
---
# <a name="evtsurpriseremovenorequestcomplete-rule-kmdf"></a>EvtSurpriseRemoveNoRequestComplete ルール (kmdf)


**EvtSurpriseRemoveNoRequestComplete**ルールでは、WDF ドライバーからの要求を完了べきではないことを指定します[ *EvtDeviceSurpriseRemoval* ](https://msdn.microsoft.com/library/windows/hardware/ff540913)コールバック、代わりに自己管理型の I/O のコールバック関数を使用する必要があります。 *EvtDeviceSurpriseRemoval*コールバックは、電源のパスと同期されていません。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>EvtSurpriseRemoveNoRequestComplete</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
 

 





