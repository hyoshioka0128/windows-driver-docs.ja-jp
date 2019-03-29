---
title: PdoInitFreeDeviceCallback ルール (kmdf)
description: PdoInitFreeDeviceCallback ルールでは、ドライバーは、framework デバイス オブジェクトの初期化関数を呼び出すときにエラーが発生した場合に、ドライバーが WdfDeviceInitFree を呼び出す必要がありますを指定します。
ms.assetid: ec38eccc-435e-4758-8bf1-27b062cf2a18
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCallback ルール (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCallback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 485949fe3308b24eebb374280487c3777bdd256c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582647"
---
# <a name="pdoinitfreedevicecallback-rule-kmdf"></a>PdoInitFreeDeviceCallback ルール (kmdf)


**PdoInitFreeDeviceCallback**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)ドライバーが任意のフレームワーク デバイス オブジェクトを呼び出すときにエラーが発生した場合初期化関数。

ドライバーでは、新しい framework デバイス オブジェクトを初期化中にエラーが発生した場合と、ドライバーが受信した場合、 [WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体への呼び出しから[ **WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)、ドライバーを呼び出す必要があります[ **WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PdoInitFreeDeviceCallback</strong>ルール。</p>
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

[**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
[**WdfDeviceInitAssignSDDLString** ](https://msdn.microsoft.com/library/windows/hardware/ff546035) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)
[**WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050) 
 [ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546057)
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546066) 
[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071)
[**WdfPdoInitAddCompatibleID** ](https://msdn.microsoft.com/library/windows/hardware/ff548776)
 [ **WdfPdoInitAddDeviceText**](https://msdn.microsoft.com/library/windows/hardware/ff548780)
[**WdfPdoInitAddHardwareID** ](https://msdn.microsoft.com/library/windows/hardware/ff548784) 
[ **WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
[**WdfPdoInitAssignDeviceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548797) 
[ **WdfPdoInitAssignInstanceID**](https://msdn.microsoft.com/library/windows/hardware/ff548799)
[**WdfPdoInitAssignRawDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548802)も参照してください
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md)
[**PdoInitFreeDeviceCreateType4** ](kmdf-pdoinitfreedevicecreatetype4.md) 
 [InitFreeNull](kmdf-initfreenull.md)
 

 





