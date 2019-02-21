---
title: UsbKmdfIrql2 ルール (kmdf)
description: UsbKmdfIrql2 ルールでは、KMDF ドライバーが正しくない、IRQL レベルで USB 固有 Ddi を呼び出す必要がありますいないことを指定します。
ms.assetid: D514B902-8F29-4D77-A26F-57DA43A045E8
ms.date: 05/21/2018
keywords:
- UsbKmdfIrql2 ルール (kmdf)
topic_type:
- apiref
api_name:
- UsbKmdfIrql2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c24ecae95639abcbafc7909fc5ca1a8ab6a20e17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557932"
---
# <a name="usbkmdfirql2-rule-kmdf"></a>UsbKmdfIrql2 ルール (kmdf)


**UsbKmdfIrql2**ルールは、KMDF ドライバー呼び出さないでください USB 固有 Ddi 不適切な IRQL でレベルを指定します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>UsbKmdfIrql2</strong>ルール。</p>
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

[**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)
[**WdfUsbInterfaceGetConfiguredSettingIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff550059) 
 [ **WdfUsbInterfaceGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550060)
[**WdfUsbInterfaceGetEndpointInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff550063) 
 [**WdfUsbInterfaceGetInterfaceNumber**](https://msdn.microsoft.com/library/windows/hardware/ff550065)
[**WdfUsbInterfaceGetNumConfiguredPipes** ](https://msdn.microsoft.com/library/windows/hardware/ff550066) 
[ **WdfUsbInterfaceGetNumEndpoints**](https://msdn.microsoft.com/library/windows/hardware/ff550068)
[**WdfUsbInterfaceGetNumSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff550070) 
 [ **WdfUsbInterfaceSelectSetting**](https://msdn.microsoft.com/library/windows/hardware/ff550073)
[**WdfUsbTargetDeviceAllocAndQueryString** ](https://msdn.microsoft.com/library/windows/hardware/ff550074)
 [ **WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)
[**WdfUsbTargetDeviceCyclePortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550080) 
 [ **WdfUsbTargetDeviceFormatRequestForControlTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff550082) 
 [ **WdfUsbTargetDeviceFormatRequestForCyclePort**](https://msdn.microsoft.com/library/windows/hardware/ff550084)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086)
 [ **WdfUsbTargetDeviceFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff550088) 
 [ **WdfUsbTargetDeviceGetDeviceDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550090)
[**WdfUsbTargetDeviceGetInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550092) 
 [ **WdfUsbTargetDeviceGetNumInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff550094)
[**WdfUsbTargetDeviceIsConnectedSynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff550095) 
 [ **WdfUsbTargetDeviceQueryString** ](https://msdn.microsoft.com/library/windows/hardware/ff550096) 
 [ **WdfUsbTargetDeviceResetPortSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550097)
[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff550098)
**](https://msdn.microsoft.com/library/windows/hardware/ff551163)
 

 





