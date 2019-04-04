---
title: InitFreeDeviceCreateType4 rule (kmdf)
description: InitFreeDeviceCreateType4 ルールでは、WdfDeviceCreate を呼び出すと、ドライバー、WDFDEVICE を受信した場合、ドライバーにエラーが発生した場合に、ドライバーが WdfDeviceInitFree を呼び出す必要がありますを指定します\_INIT 構造への呼び出しWdfControlDeviceInitAllocate します。
ms.assetid: 5a521053-5d31-4e4a-8a82-48206d506916
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCreateType4 rule (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCreateType4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f3ad8a395659572bfeb514f3fc79cc8cd4fa9a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537707"
---
# <a name="initfreedevicecreatetype4-rule-kmdf"></a>InitFreeDeviceCreateType4 rule (kmdf)


**InitFreeDeviceCreateType4**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)ドライバーでは、呼び出し中にエラーが発生した場合[**WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)ドライバーが受信した場合と、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951) への呼び出しから構造[ **WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>InitFreeDeviceCreateType4</strong>ルール。</p>
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

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)も参照してください
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**PdoInitFreeDeviceCallback** ](kmdf-pdoinitfreedevicecallback.md) 
 [ **PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md)
[**PdoInitFreeDeviceCreateType4** ](kmdf-pdoinitfreedevicecreatetype4.md) 
 [ **InitFreeNull**](kmdf-initfreenull.md)
 

 





