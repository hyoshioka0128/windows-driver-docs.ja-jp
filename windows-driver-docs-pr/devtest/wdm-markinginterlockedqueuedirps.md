---
title: MarkingInterlockedQueuedIrps ルール (wdm)
description: MarkingInterlockedQueuedIrps ルールでは、前に、さらに処理するため、インタロックされた形式でキュー、ドライバーがその保留中として IRP を正しくマークすることを指定します。
ms.assetid: a065b28f-f02a-45af-b9d9-754a36519b99
ms.date: 05/21/2018
keywords:
- MarkingInterlockedQueuedIrps ルール (wdm)
topic_type:
- apiref
api_name:
- MarkingInterlockedQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35eb90dcf17ab43520e159d61b524829772a380c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331347"
---
# <a name="markinginterlockedqueuedirps-rule-wdm"></a>MarkingInterlockedQueuedIrps ルール (wdm)


**MarkingInterlockedQueuedIrps**ルールでは、前に保留中、キューにそれをさらに処理するためのインタロックされた方法でと、ドライバーがその IRP を正しくマークことを指定します。

このルールは、ドライバーを呼び出すことを指定しますも[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)し呼び出します IRP をインタロックされたキューに追加するには、次の関数のいずれかの前に保留中として、IRP を正しくマークします。

-   [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)

-   [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)

-   [**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)

ドライバーを呼び出す必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)インタロックされたキューに複数の処理が必要な IRP を追加する前にします。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

詳細については、次を参照してください。 [**同期 IRP キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff564531)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MarkingInterlockedQueuedIrps</strong>ルール。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
 [ **RemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff561032)も参照してください
--------

[**MarkIrpPending**](wdm-markirppending.md)
[**IRP のキャンセルを同期します。**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





