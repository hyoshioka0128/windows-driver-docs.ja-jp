---
title: PeriodicTimer ルール (ndis)
description: PeriodicTimer ルールでは、IRQL パッシブで NdisCancelTimerObject の呼び出し元を実行する必要がありますを指定します\_NdisSetTimerObject 関数の MillisecondsPeriod パラメーターに 0 以外の値が指定されている場合のレベルします。
ms.assetid: a6bda698-5150-4fd5-b665-d460b88fe0ac
ms.date: 05/21/2018
keywords:
- PeriodicTimer ルール (ndis)
topic_type:
- apiref
api_name:
- PeriodicTimer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27d83173e1ce4e77c338156626bccd91e5e8c89b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574677"
---
# <a name="periodictimer-rule-ndis"></a>PeriodicTimer ルール (ndis)


**PeriodicTimer**ルールを指定する、呼び出し元の[ **NdisCancelTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561624)で実行する必要があります**IRQL = パッシブ\_レベル**で 0 以外の値が指定されている場合、 *MillisecondsPeriod*のパラメーター、 [ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)関数。 場合、 *MillisecondsPeriod*のパラメーター、 **NdisSetTimerObject**関数がゼロ、呼び出し元の**NdisCancelTimerObject**で実行されている**IRQL&lt;= ディスパッチ\_レベル**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PeriodicTimer</strong>ルール。</p>
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

[**NdisCancelTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561624)
[**NdisSetTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff564563)
 

 





