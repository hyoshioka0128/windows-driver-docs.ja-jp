---
title: DeviceInitAPI ルール (kmdf)
description: FDO デバイスの場合、ドライバーがデバイスオブジェクトの WdfDeviceCreate メソッドを呼び出す前に、フレームワークのデバイスオブジェクト初期化メソッドとフレームワーク FDO 初期化メソッドを呼び出す必要があります。
ms.assetid: 526807b8-748e-4bc1-b795-9971ed98509c
ms.date: 05/21/2018
keywords:
- DeviceInitAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- DeviceInitAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2413cac19434e17f875f44839d04cc00d38037e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839513"
---
# <a name="deviceinitapi-rule-kmdf"></a>DeviceInitAPI ルール (kmdf)


FDO デバイスの場合、ドライバーがデバイスオブジェクトの[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)メソッドを呼び出す前に、フレームワークのデバイスオブジェクト初期化メソッドとフレームワーク FDO 初期化メソッドを呼び出す必要があります。

FDO デバイスの場合は、フレームワークのデバイスオブジェクトの初期化メソッドとフレームワークの FDO の初期化メソッドを使用して、 [Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体に情報を格納します。これにより、ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出した後に呼び出すことはできません。フレームワークデバイスオブジェクト。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>deviceinitapi</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)  
[**Wdfdeviceinit割り当て名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)  
[**Wdfdeviceinit割り当て Sddlstring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)  
[**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)  
[**WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback)  
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)  
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)  
[**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)  
[**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)  
[**WdfDeviceInitSetDeviceType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdevicetype)  
[**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)  
[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)  
[**WdfDeviceInitSetIoInCallerContextCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)  
[**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)  
[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)  
[**WdfDeviceInitSetPowerInrush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerinrush)  
[**WdfDeviceInitSetPowerNotPageable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowernotpageable)  
[**WdfDeviceInitSetPowerPageable 可能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpageable)  
[**WdfDeviceInitSetPowerPolicyEventCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)  
[**WdfDeviceInitSetPowerPolicyOwnership 所有権**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)  
[**WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)  
[**WdfFdoInitAllocAndQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandqueryproperty)  
[**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)  
[**WdfFdoInitQueryProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitqueryproperty)  
[**WdfFdoInitSetDefaultChildListConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)  
[**WdfFdoInitSetEventCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitseteventcallbacks)  
[**WdfFdoInitSetFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)  
[**WdfFdoInitWdmGetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitwdmgetphysicaldevice)  
 

 





