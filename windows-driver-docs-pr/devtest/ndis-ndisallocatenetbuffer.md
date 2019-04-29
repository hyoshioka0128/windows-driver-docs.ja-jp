---
title: NdisAllocateNetBuffer ルール (ndis)
description: NdisAllocateNetBuffer ルールでは、NdisAllocateNetBuffer と NdisFreeNetBuffer が異なる順序でと呼ばれることを指定します。 最終的な目標は、NET のすべてのインスタンスを確認する\_MiniportHaltEx の終了時にバッファーが解放されます。
ms.assetid: 218708DA-ADDF-4E59-900A-4F8B5CBF00B7
ms.date: 05/21/2018
keywords:
- NdisAllocateNetBuffer ルール (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateNetBuffer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc2231b09125a3f3be37a2a52f98cf357f7eea11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387437"
---
# <a name="ndisallocatenetbuffer-rule-ndis"></a>NdisAllocateNetBuffer ルール (ndis)


**NdisAllocateNetBuffer**ルールを指定する[ **NdisAllocateNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff561607)と[ **NdisFreeNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562582)代替の順序で呼び出されます。 すべてのインスタンスを確認する最終目標は、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)ときに解放される[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が終了します。

ルールは、3 つの異なる状態を使用します。 状態が変更されたときに、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)割り当てまたは解放します。 場合、 **NET\_バッファー**ときに割り当てられたまま、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)終了すると、ルールは、障害を報告します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisAllocateNetBuffer</strong>ルール。</p>
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

[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)
[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)
 

 





