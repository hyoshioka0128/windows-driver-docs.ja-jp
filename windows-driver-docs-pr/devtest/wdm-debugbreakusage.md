---
title: DebugBreakUsage ルール (wdm)
description: DebugBreakUsage ルールでは、ドライバーでは DbgBreakPoint または DbgBreakPointWithStatus を呼び出す必要がないことを指定します。 このルールは、非デバッグ バージョンのドライバーをビルドする場合にのみ適用されます。
ms.assetid: 1f634b7c-6939-41ea-8eed-5207f40e5476
ms.date: 05/21/2018
keywords:
- DebugBreakUsage ルール (wdm)
topic_type:
- apiref
api_name:
- DebugBreakUsage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 340b9e2bf8e8c132dcf42ed364b10bcb9ffb7579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363393"
---
# <a name="debugbreakusage-rule-wdm"></a>DebugBreakUsage ルール (wdm)


**DebugBreakUsage**ルールでは、ドライバーを呼び出してはならないことを指定します[ **DbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff543626)または[ **DbgBreakPointWithStatus**](https://msdn.microsoft.com/library/windows/hardware/ff543629). このルールは、非デバッグ バージョンのドライバーをビルドする場合にのみ適用されます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DebugBreakUsage</strong>ルール。</p>
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

 

 





