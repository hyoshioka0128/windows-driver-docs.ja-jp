---
title: PdoInitFreeDeviceCreate ルール (kmdf)
description: PdoInitFreeDeviceCreate ルールでは、デバイス オブジェクトの初期化関数のいずれかでエラーが発生した場合と、ドライバー、WDFDEVICE を受信した場合に、ドライバーが WdfDeviceCreate ではなく WdfDeviceInitFree を呼び出す必要がありますを指定します\_INIT 構造から、WdfPdoInitAllocate を呼び出します。
ms.assetid: d73401dd-ec96-4870-9f6d-aa399deab173
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCreate ルール (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87b9e76a0037e2ce4e9d02a7a4ceb7aa7b3b8be3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384108"
---
# <a name="pdoinitfreedevicecreate-rule-kmdf"></a>PdoInitFreeDeviceCreate ルール (kmdf)


**PdoInitFreeDeviceCreate**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)の代わりに[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)デバイス オブジェクトの初期化関数のいずれかでエラーが発生した場合と、ドライバーの受信、WDFDEVICE 場合\_INIT 構造体への呼び出しから[ **WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786).

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PdoInitFreeDeviceCreate</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
[**WdfDeviceInitAssignSDDLString** ](https://msdn.microsoft.com/library/windows/hardware/ff546035) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043) 
 [ **WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546057) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)
[**WdfDeviceInitRegisterPowerStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546071)
 [ **WdfPdoInitAddCompatibleID**](https://msdn.microsoft.com/library/windows/hardware/ff548776)
[**WdfPdoInitAddDeviceText** ](https://msdn.microsoft.com/library/windows/hardware/ff548780) 
[ **WdfPdoInitAddHardwareID**](https://msdn.microsoft.com/library/windows/hardware/ff548784)
[**WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786) 
[ **WdfPdoInitAssignDeviceID**](https://msdn.microsoft.com/library/windows/hardware/ff548797)
[**WdfPdoInitAssignInstanceID** ](https://msdn.microsoft.com/library/windows/hardware/ff548799) 
 [ **WdfPdoInitAssignRawDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548802)も参照してください
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md)
[**PdoInitFreeDeviceCreateType4** ](kmdf-pdoinitfreedevicecreatetype4.md) 
 [ **InitFreeNull**](kmdf-initfreenull.md)
 

 





