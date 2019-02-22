---
title: IoReuseIrp ルール (wdm)
description: IoReuseIrp ルールでは、ドライバーが IoReuseIrp を IoAllocateIrp で以前に割り当てられた Irp でのみ使用することを指定します。
ms.assetid: E927D12D-03DE-41D7-B130-BA86F0C0CB8A
ms.date: 05/21/2018
keywords:
- IoReuseIrp ルール (wdm)
topic_type:
- apiref
api_name:
- IoReuseIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1cdad946e603a13c2a1325e5e92bc9c4853f1e35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559742"
---
# <a name="ioreuseirp-rule-wdm"></a>IoReuseIrp ルール (wdm)


**IoReuseIrp**ルールでは、ドライバーを使用することを指定します[ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661)で以前割り当てられた Irp でのみ[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoReuseIrp</strong>ルール。</p>
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
[**InsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff547820)
[**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257) 
 [ **IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)
[**IoCsqInsertIrpEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549067)
 [ **IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)
[**IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661) 
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





