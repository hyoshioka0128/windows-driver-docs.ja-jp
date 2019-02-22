---
title: NdisAllocateMdl ルール (ndis)
description: NdisAllocateMdl ルールでは、NdisAllocateMdl と NdisFreeMdl が異なる順序でと呼ばれることを指定します。 最終的な目標では、MiniportHaltEx が終了したときにすべて MDLs が解放されるかどうかを確認します。
ms.assetid: 8146E72B-0B63-4224-9677-5E6FEFCEB745
ms.date: 05/21/2018
keywords:
- NdisAllocateMdl ルール (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateMdl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bddec8bb956862bb633611b68732a32a6345bd19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557163"
---
# <a name="ndisallocatemdl-rule-ndis"></a>NdisAllocateMdl ルール (ndis)


**NdisAllocateMdl**ルールを指定する[ **NdisAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff561605)と[ **NdisFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff562575)は代替の順序で呼び出されます。 最終的な目標はすべて MDLs いることを確認するときに解放される[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が終了します。

ルールは、3 つの異なる状態を使用します。 MDL の割り当てまたは解放時の状態の変更。 場合は、MDL がまだ割り当てられているときに、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)終了すると、ルールは、障害を報告します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisAllocateMdl</strong>ルール。</p>
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

[**NdisAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff561605)
[**NdisFreeMdl**](https://msdn.microsoft.com/library/windows/hardware/ff562575)
 

 





