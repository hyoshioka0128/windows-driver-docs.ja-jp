---
title: Init\_NdisAllocateIoWorkItem ルール (ndis)
description: Init\_NdisAllocateIoWorkItem ルール NdisAllocateIoWorkItem が MiniportInitializeEx 中に少なくとも 1 回呼び出されると、NdisFreeIoWorkItem 関数にする必要があります呼び出すように指定を少なくとも 1 回、MPHaltEx で場合 MiniportInitializeEx。成功します。
ms.assetid: B7889948-741C-4C54-B27F-3175ED4EA7BA
ms.date: 05/21/2018
keywords:
- Init_NdisAllocateIoWorkItem ルール (ndis)
topic_type:
- apiref
api_name:
- Init_NdisAllocateIoWorkItem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c6c7be6519d240e2862517c446ec95e381a8a7c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531940"
---
# <a name="initndisallocateioworkitem-rule-ndis"></a>Init\_NdisAllocateIoWorkItem ルール (ndis)


**Init\_NdisAllocateIoWorkItem**規則で指定された場合[ **NdisAllocateIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561604)中に少なくとも 1 回呼び出される[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)、 [ **NdisFreeIoWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff561855)関数にする必要があります。

-   - 場合に、MPHaltEx で少なくとも 1 回呼び出すこと[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)が成功するとします。
-   - 呼び出される[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)場合は、 *MiniportInitializeEx*は失敗します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Init_NdisAllocateIoWorkItem</strong>ルール。</p>
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

[**NdisAllocateIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561604)
[**NdisFreeIoWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff561855)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





