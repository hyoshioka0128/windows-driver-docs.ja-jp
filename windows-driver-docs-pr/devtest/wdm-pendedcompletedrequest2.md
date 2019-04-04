---
title: PendedCompletedRequest2 rule (wdm)
description: PendedCompletedRequest2 ルールでは、待機が必要である呼び出しの後に、保留または PoCallDriver ディスパッチ ルーチンは保留中の IRP を済ませるためにを指定します。
ms.assetid: 738B9DEE-D7D4-4E6A-AE2D-F363F1255E8A
ms.date: 05/21/2018
keywords:
- PendedCompletedRequest2 rule (wdm)
topic_type:
- apiref
api_name:
- PendedCompletedRequest2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddfc32a0f63400b7d78ef142a4e5a411919649a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548900"
---
# <a name="pendedcompletedrequest2-rule-wdm"></a>PendedCompletedRequest2 rule (wdm)


**PendedCompletedRequest2**ルールの呼び出しの後に待機が必要なことを指定します[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)ディスパッチ ルーチンは保留中の IRP を済ませるためです。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PendedCompletedRequest2</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





