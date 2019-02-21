---
title: NdisMDeregisterInterruptEx ルール (ndis)
description: NdisMDeregisterInterruptEx が制御を返した後、ミニポート ドライバーは NdisMSynchronizeWithInterruptEx 関数を呼び出すことはできません。
ms.assetid: 49AC090C-157C-4CD2-9C7A-BDD5F3C6D58F
ms.date: 05/21/2018
keywords:
- NdisMDeregisterInterruptEx ルール (ndis)
topic_type:
- apiref
api_name:
- NdisMDeregisterInterruptEx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca0edc2418941e04fc0cd761b98a2466fadf868a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532872"
---
# <a name="ndismderegisterinterruptex-rule-ndis"></a>NdisMDeregisterInterruptEx ルール (ndis)


後[ **NdisMDeregisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575)コントロールを返します、ミニポート ドライバーを呼び出すことはできません、 [ **NdisMSynchronizeWithInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563681)関数。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisMDeregisterInterruptEx</strong>ルール。</p>
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

[**NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)
[**NdisMRegisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563649)
[**NdisMSynchronizeWithInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563681)
 

 





