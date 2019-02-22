---
title: ReqSendFail ルール (kmdf)
description: ReqSendFail ルールでは、ドライバーが WdfRequestSend メソッドが失敗する場合に適切な完了状態を設定する必要がありますを指定します。
ms.assetid: 324e0351-5879-4d10-a877-1da9b7424c4e
ms.date: 05/21/2018
keywords:
- ReqSendFail ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqSendFail
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c5b085dc37f4282d7a02694d204d290068d89c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551388"
---
# <a name="reqsendfail-rule-kmdf"></a>ReqSendFail ルール (kmdf)


**ReqSendFail**ルールでは、ドライバーがの場合に適切な完了状態を設定する必要がありますを指定します、 [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)メソッドが失敗する可能性があります。

[**WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)返せる**FALSE**場合でも、要求の送信に失敗した場合、WDF\_要求\_送信\_オプション\_送信\_\_破棄フラグは、ドライバーの要求オプションで設定します。 このような場合は、ドライバーは、呼び出すことによって、適切な完了の状態要求を完了する必要があります[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)、または呼び出すことによって[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqSendFail</strong>ルール。</p>
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

[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestReuse**](https://msdn.microsoft.com/library/windows/hardware/ff550026) 
 [ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
 

 





