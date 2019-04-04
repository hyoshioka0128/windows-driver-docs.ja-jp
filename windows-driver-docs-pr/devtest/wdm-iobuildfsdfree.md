---
title: IoBuildFsdFree ルール (wdm)
description: IoBuildFsdFree ルールでは、ドライバーが Irp が以前に割り当てられた IoBuildAsynchronousFsdRequest とでのみ IoFreeIrp を使用することを指定します。
ms.assetid: F507CD5C-88F9-4EEA-BB41-40F2728CAA85
ms.date: 05/21/2018
keywords:
- IoBuildFsdFree ルール (wdm)
topic_type:
- apiref
api_name:
- IoBuildFsdFree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e989dfce52272e71665a51680d5d8279ce4e341
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531633"
---
# <a name="iobuildfsdfree-rule-wdm"></a>IoBuildFsdFree ルール (wdm)


**IoBuildFsdFree**ルールでは、ドライバーを使用することを指定します[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)で以前割り当てられた Irp でのみ[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoBuildFsdFree</strong>ルール。</p>
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

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)
[**IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)
 

 





