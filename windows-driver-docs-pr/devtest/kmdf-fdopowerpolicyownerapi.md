---
title: FDOPowerPolicyOwnerAPI 規則 (kmdf)
description: FDOPowerPolicyOwnerAPI ルールでは、FDO ドライバーが電源ポリシーの所有権を放棄した場合、WdfDeviceInitSetPowerPolicyEventCallbacks バック、WdfDeviceAssignS0IdleSettings、WdfDeviceAssignSxWakeSettings の各メソッドは、ドライバーが電源ポリシーの所有者である実行パスでのみ呼び出すことができます。 SDV は、このルールに対して警告を発行します。
ms.assetid: b0695dff-070c-4c55-a71d-a78fc45eb805
ms.date: 05/21/2018
keywords:
- FDOPowerPolicyOwnerAPI 規則 (kmdf)
topic_type:
- apiref
api_name:
- FDOPowerPolicyOwnerAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8629df7588edbb23e0b891434866a9d51d7b77d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917071"
---
# <a name="fdopowerpolicyownerapi-rule-kmdf"></a>FDOPowerPolicyOwnerAPI 規則 (kmdf)


**Fdopowerpolicyownerapi**ルールでは、FDO ドライバーが電源ポリシーの所有権を放棄した場合、 [**Wdfdeviceinitsetpowerpolicyeventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)、 [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)、 [**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings)の各メソッドは、ドライバーが電源ポリシーの所有者である実行パスでのみ呼び出すことができます。 SDV は、このルールに対して警告を発行します。

FDO ドライバーが、2番目のパラメーターの値として**FALSE**を指定して[**Wdfdeviceinitsetpowerpolicyownership**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)メソッドを呼び出すと、そのドライバーによって[**Wdfdeviceinitsetpowerpolicyeventcalls**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)、 **WdfDeviceAssignS0IdleSettings**、および**WdfDeviceAssignSxWakeSettings**を呼び出すと、規則違反と警告メッセージが表示されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Fdopowerpolicyownerapi</strong>規則を指定します。</p>
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

[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) 
[**WdfDeviceAssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignsxwakesettings) 
[**Wdfdeviceinitsetpowerpolicyeventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks) 
[**Wdfdeviceinitsetpowerpolicyownership 所有権**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyownership)
 

 





