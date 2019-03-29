---
title: ReqSendWhileSpinlock ルール (kmdf)
description: ReqSendWhileSpinlock ルールでは、要求が送信されなかったこと、ドライバーは、スピン ロックを保持している間を指定します。
ms.assetid: f038f4ca-aa24-4df3-9c31-d8eec928c306
ms.date: 05/21/2018
keywords:
- ReqSendWhileSpinlock ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqSendWhileSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9b08f4071a5973f9efdb38daa54798bfd9af829
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577685"
---
# <a name="reqsendwhilespinlock-rule-kmdf"></a>ReqSendWhileSpinlock ルール (kmdf)


**ReqSendWhileSpinlock**ルールでは、要求が送信されなかったこと、ドライバーは、スピン ロックを保持している間を指定します。

ドライバーは、スピンロックを保持している間、すべての要求を送信する場合は、デッドロックが発生するまたはも下位のドライバーは、ロックの取得、または共有リソースにアクセスしようとすると、要求を受信する下位のドライバーとの調和ができませんでした。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqSendWhileSpinlock</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)
[**WdfSpinLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff550044) 
 [ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)を参照してくださいまた
--------

[I/O 要求の完了](https://msdn.microsoft.com/library/windows/hardware/ff540740)
[キャンセルおよび終了コードを同期します。](https://msdn.microsoft.com/library/windows/hardware/ff544726)
 

 





