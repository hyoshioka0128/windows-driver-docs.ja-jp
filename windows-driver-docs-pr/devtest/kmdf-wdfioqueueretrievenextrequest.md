---
title: WdfIoQueueRetrieveNextRequest ルール (kmdf)
description: WdfIoQueueRetrieveNextRequest ルールでは、WdfIoQueueFindRequest が呼び出された後に、WdfIoQueueRetrieveNextRequest が呼び出されないことを指定します。
ms.assetid: D6BB8920-16A1-4E87-A904-137ACAB7418A
ms.date: 05/21/2018
keywords:
- WdfIoQueueRetrieveNextRequest ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfIoQueueRetrieveNextRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a552a0058853674bc71b964af198fa1b1290bc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559729"
---
# <a name="wdfioqueueretrievenextrequest-rule-kmdf"></a>WdfIoQueueRetrieveNextRequest ルール (kmdf)


**WdfIoQueueRetrieveNextRequest**ルールを指定する[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)後は呼び出されません[ **WdfIoQueueFindRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547415)が呼び出されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WdfIoQueueRetrieveNextRequest</strong>ルール。</p>
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

[**WdfIoQueueFindRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547415)
[**WdfIoQueueRetrieveNextRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548462)
 

 





