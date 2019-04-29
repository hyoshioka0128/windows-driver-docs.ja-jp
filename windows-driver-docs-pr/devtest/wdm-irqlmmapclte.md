---
title: IrqlMmApcLte ルール (wdm)
ms.assetid: 075f5710-b2bf-4546-9648-661a3c8521f8
ms.date: 05/21/2018
description: ''
keywords:
- IrqlMmApcLte ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlMmApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb212f8a9b4f230641de54ddb3fe703a5d756efa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331372"
---
# <a name="irqlmmapclte-rule-wdm"></a>IrqlMmApcLte ルール (wdm)


**IrqlMmApcLte**ルールを指定するドライバー ルーチンを呼び出して次のメモリ マネージャー IRQL で実行されている場合にのみ&lt;APC を =\_レベル。

-   [**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)

-   [**MmFreeNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554516)

-   [**MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)

-   [**MmFreePagesFromMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554521)

-   [**MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)

-   [**MmLockPagableSectionByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff554610)

-   [**MmPageEntireDriver**](https://msdn.microsoft.com/library/windows/hardware/ff554650)

-   [**MmResetDriverPaging**](https://msdn.microsoft.com/library/windows/hardware/ff554680)

-   [**MmSecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556374)

-   [**MmUnlockPagableImageSection**](https://msdn.microsoft.com/library/windows/hardware/ff556377)

-   [**MmUnsecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556395)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020019) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlMmApcLte</strong>ルール。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)
[**MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)
[**MmAllocatePagesForMdlEx** ](https://msdn.microsoft.com/library/windows/hardware/ff554489) 
 [ **MmFreeNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554516)
[**MmFreePagesFromMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554521) 
 [ **MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)
[**MmLockPagableSectionByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff554610) 
 [ **MmPageEntireDriver**](https://msdn.microsoft.com/library/windows/hardware/ff554650)
[**MmResetDriverPaging** ](https://msdn.microsoft.com/library/windows/hardware/ff554680) 
 [ **MmSecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556374)
[**MmUnlockPagableImageSection** ](https://msdn.microsoft.com/library/windows/hardware/ff556377) 
 [ **MmUnsecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556395)
 

 





