---
title: ReqMarkCancelableSend ルール (kmdf)
description: ReqMarkCancelableSend ルールでは、ドライバーによって転送された要求が WdfRequestMarkCancelable を呼び出すことによってキャンセル可能なとしてマークされないことを指定します。
ms.assetid: 8fb40977-7a34-4bb8-ba98-16e98fbd9137
ms.date: 05/21/2018
keywords:
- ReqMarkCancelableSend ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqMarkCancelableSend
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1220db107776f737062e60b0c1bdb9e7b8701ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536906"
---
# <a name="reqmarkcancelablesend-rule-kmdf"></a>ReqMarkCancelableSend ルール (kmdf)


**ReqMarkCancelableSend**規則を指定、ドライバーによって転送された要求マークされていないとキャンセル可能な呼び出して[ **WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983)します。

キャンセル可能なとして要求をマークするには、ドライバーは、要求を所有する必要があります。 以前のドライバが不要になった所有権を保持し、呼び出す必要があります、要求が別のドライバーに送信されると、 [ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)キャンセル可能なマークされている以前の場合、要求にします。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqMarkCancelableSend</strong>ルール。</p>
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

[**WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983)
[**WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027) 
 [ **WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)
 

 





