---
title: NonPnPDrvPowerPolicyOwnerAPI ルール (kmdf)
description: NonPnPDrvPowerPolicyOwnerAPI ルールでは、非 PnP ドライバーが電源管理に関連する特定の Ddi を呼び出すことはできませんを指定します。
ms.assetid: d15211d2-cf53-4b60-bd26-a6c82d50bd42
ms.date: 05/21/2018
keywords:
- NonPnPDrvPowerPolicyOwnerAPI ルール (kmdf)
topic_type:
- apiref
api_name:
- NonPnPDrvPowerPolicyOwnerAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a6cec10d51dd4f71d76108263b1b3f6516caba19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582572"
---
# <a name="nonpnpdrvpowerpolicyownerapi-rule-kmdf"></a>NonPnPDrvPowerPolicyOwnerAPI ルール (kmdf)


**NonPnPDrvPowerPolicyOwnerAPI**ルールでは、非 PnP ドライバーが電源管理に関連する特定の Ddi を呼び出すことはできませんを指定します。

ドライバーが登録していない場合、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数では、次の Ddi を呼び出すことができません。

[**WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)
[**WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774) 
 [ **WdfDeviceAssignSxWakeSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545909)
[**WdfDeviceGetDevicePowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff545985) 
 [ **WdfDeviceGetDevicePowerPolicyState**](https://msdn.microsoft.com/library/windows/hardware/ff545974)
[**WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135) 
 [ **WdfDeviceInitSetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546776)
[**WdfDeviceInitRegisterPowerStateChangeCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546071)
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546066)
[**WdfDeviceInitSetPowerNotPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546147) 
 [ **WdfDeviceInitSetPowerPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546766)
[**WdfDeviceInitSetPowerInrush** ](https://msdn.microsoft.com/library/windows/hardware/ff546142) 
 [ **WdfDeviceSetPowerCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff546901)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NonPnPDrvPowerPolicyOwnerAPI</strong>ルール。</p>
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









