---
title: InitFreeDeviceCreate ルール (kmdf)
description: InitFreeDeviceCreate ルールでは、デバイス オブジェクトの初期化メソッドのいずれかでエラーが発生した場合と、ドライバー、WDFDEVICE を受信した場合に、ドライバーが WdfDeviceCreate ではなく WdfDeviceInitFree を呼び出す必要がありますを指定します\_呼び出しからの初期化構造体WdfControlDeviceInitAllocate します。
ms.assetid: 9d33bd42-8781-442e-9c7d-00b6f04b1634
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCreate ルール (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 526e54024dae7d385b8d630ad82973c38fe6daad
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393251"
---
# <a name="initfreedevicecreate-rule-kmdf"></a>InitFreeDeviceCreate ルール (kmdf)


**InitFreeDeviceCreate**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)の代わりに[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)デバイス オブジェクトの初期化メソッドのいずれかでエラーが発生した場合と、ドライバーが受信した場合、 [ **WDFDEVICE\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init) への呼び出しの構造[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>InitFreeDeviceCreate</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)
[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)
[**WdfDeviceInitAssignName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname) 
 [ **WdfDeviceInitAssignSDDLString** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)
[**WdfDeviceInitFree** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree) 
 [ **WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback) 
[ **WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)
[**WdfPdoInitAddCompatibleID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)
 [ **WdfPdoInitAddDeviceText**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext)
[**WdfPdoInitAddHardwareID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)
 [ **WdfPdoInitAssignDeviceID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)
[**WdfPdoInitAssignInstanceID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid) 
 [ **WdfPdoInitAssignRawDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)も参照してください
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md)
[**PdoInitFreeDeviceCreate** ](kmdf-pdoinitfreedevicecreate.md) 
 [ **PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md)
[**InitFreeNull**](kmdf-initfreenull.md)
 

 





