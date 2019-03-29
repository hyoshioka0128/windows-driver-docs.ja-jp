---
title: InitFreeDeviceCallback ルール (kmdf)
description: InitFreeDeviceCallback ルールでは、ドライバーはドライバーでは、新しい framework デバイス オブジェクトを初期化中にエラーが発生した場合と、ドライバー、WDFDEVICE を受信する場合は WdfDeviceInitFree を呼び出す必要がありますを指定します\_INIT 構造への呼び出しWdfControlDeviceInitAllocate します。
ms.assetid: 518f60cf-283a-4924-8bbd-2f5e26d3e850
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCallback ルール (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCallback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f4d63598cac4ae13253d148c5ae31ba9f5bd0da5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573051"
---
# <a name="initfreedevicecallback-rule-kmdf"></a>InitFreeDeviceCallback ルール (kmdf)


InitFreeDeviceCallback ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)ドライバーでは、新しい framework デバイス オブジェクトを初期化中にエラーが発生した場合と、ドライバーが受信した場合[ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体への呼び出しから[ **WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>InitFreeDeviceCallback</strong>ルール。</p>
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

[**WdfControlDeviceInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff545841)
[**WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029) 
 [ **WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)
[**WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) 
 [**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546057) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546071) 
 [ **WdfPdoInitAddCompatibleID**](https://msdn.microsoft.com/library/windows/hardware/ff548776)
[**WdfPdoInitAddDeviceText** ](https://msdn.microsoft.com/library/windows/hardware/ff548780)
 [ **WdfPdoInitAddHardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff548784)
[**WdfPdoInitAssignDeviceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548797)
 [ **WdfPdoInitAssignInstanceID**](https://msdn.microsoft.com/library/windows/hardware/ff548799)
[**WdfPdoInitAssignRawDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548802)
 

 





