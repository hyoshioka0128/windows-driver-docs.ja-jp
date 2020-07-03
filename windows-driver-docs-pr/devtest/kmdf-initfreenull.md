---
title: InitFreeNull ルール (kmdf)
description: InitFreeNull 規則は、 \_ WDFDEVICE init 構造体への NULL ポインターを使用して、DDIs をパラメーターとして受け取ることができないことを指定し \_ ます。
ms.assetid: 99ced415-9af9-4d06-a10f-4c960897ad5f
ms.date: 05/21/2018
keywords:
- InitFreeNull ルール (kmdf)
topic_type:
- apiref
api_name:
- InitFreeNull
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1bda90fa27f34dfad9892a18b473986ca892f512
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916989"
---
# <a name="initfreenull-rule-kmdf"></a>InitFreeNull ルール (kmdf)


**InitFreeNull**規則は、 \_ [wdfdevice \_ Init](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体への**NULL**ポインターを使用して、DDIs をパラメーターとして受け取ることができないことを指定します。

フレームワークによって提供されるメソッドは、 [Wdfdevice \_ INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を初期化します。 ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、機能しているデバイスオブジェクト (FDO) または物理デバイスオブジェクト (PDO) を作成する場合、成功した場合、 **WdfDeviceCreate**メソッドは最初のパラメーターを**NULL**に設定します。

ドライバーがデバイスオブジェクトの初期化メソッドまたは[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すときにエラーが発生した場合、ドライバーは WdfDeviceInitFree を呼び出す必要があります。 WdfDeviceInitFree を正常に呼び出した後、 [Wdfdevice \_ init](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体へのポインターを**null** (pwdfdevice \_ init =**null**) に設定する必要があります。

**ドライバーモデル: KMDF**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>InitFreeNull</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
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
[**Wdfdeviceinitfree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree) 
[**WdfDeviceInitRegisterPnpStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback) 
[**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback) 
[**WdfDeviceInitRegisterPowerStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback) 
[**Wdfpdoinitadd互換 id**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid) 
[**Wdfpdoinitadddevicetext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext) 
[**WdfPdoInitAddHardwareID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid) 
[**Wdfpdoinit割り当て deviceid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid) 
[**Wdfpdoinit割り当て instanceid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid) 
[**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)関連項目
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md) 
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md) 
[**InitFreeDeviceCreateType2**](kmdf-initfreedevicecreatetype2.md) 
[**PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md) 
[**InitFreeDeviceCreateType4**](kmdf-initfreedevicecreatetype4.md) 
[**PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md) 
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md)
 

 





