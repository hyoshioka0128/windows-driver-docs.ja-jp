---
title: PdoInitFreeDeviceCreateType4 rule (kmdf)
description: PdoInitFreeDeviceCreateType4 ルールでは、ドライバーが WdfDeviceCreate を呼び出すときにエラーが発生した場合に、ドライバーが WdfDeviceInitFree を呼び出す必要がありますを指定します。
ms.assetid: 9293f293-7de6-476a-ab35-09174b7b3480
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCreateType4 rule (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCreateType4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24ff7cb0c9ee3de74373f08a1bd017cb086ecc79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579579"
---
# <a name="pdoinitfreedevicecreatetype4-rule-kmdf"></a>PdoInitFreeDeviceCreateType4 rule (kmdf)


PdoInitFreeDeviceCreateType4 ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)ドライバーを呼び出すときにエラーが発生した場合[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926).

呼び出すときに、ドライバーにエラーが発生した場合[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)、ドライバーが受信した場合と、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951) への呼び出しの構造[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)、ドライバーを呼び出す必要があります[ **WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PdoInitFreeDeviceCreateType4</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
 

 





