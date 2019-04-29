---
title: PendedCompletedRequest3 rule (wdm)
description: PendedCompletedRequest3 ルールでは、保留中の IRP を IoCompleteRequest への呼び出しで完了しない必要がありますを指定します。
ms.assetid: 051D8E8C-4C06-4497-A099-D038DC9152FA
ms.date: 05/21/2018
keywords:
- PendedCompletedRequest3 rule (wdm)
topic_type:
- apiref
api_name:
- PendedCompletedRequest3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be6a8db8c7b151c7303e5a61de382f231eda4498
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325827"
---
# <a name="pendedcompletedrequest3-rule-wdm"></a>PendedCompletedRequest3 rule (wdm)


**PendedCompletedRequest3**ルールでは、保留中の IRP がへの呼び出しで完了しない必要がありますを指定します[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PendedCompletedRequest3</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)
 [ **Kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) 
 [**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





