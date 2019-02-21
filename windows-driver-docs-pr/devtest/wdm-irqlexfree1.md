---
title: IrqlExFree1 ルール (wdm)
description: IrqlExFree1 ルールでは、適切な IRQL で ExFreePool と ExFreePoolWithTag と呼ばれることを指定します。
ms.assetid: D0ECF4C3-8207-4618-949E-D80DBC38DBE3
ms.date: 05/21/2018
keywords:
- IrqlExFree1 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlExFree1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b21eda9c2b29a9a107d1f80a54e0c6c7de5bd1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536235"
---
# <a name="irqlexfree1-rule-wdm"></a>IrqlExFree1 ルール (wdm)


**IrqlExFree1**ルールを指定する[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)と[ **ExFreePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544593)と呼ばれます適切な IRQL します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlExFree1</strong>ルール。</p>
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

[**Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExFreePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544593)
 

 





