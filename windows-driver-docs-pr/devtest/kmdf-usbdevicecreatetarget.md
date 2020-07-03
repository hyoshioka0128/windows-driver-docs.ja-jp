---
title: UsbDeviceCreateTarget ルール (kmdf)
description: UsbDeviceCreateTarget ルールでは、現在デバイスコンテキストにある WDFUSBDEVICE オブジェクトがリークしている間に、複数の WDFUSBDEVICE オブジェクトが作成されないことを指定します。
ms.assetid: c2617c2b-553e-44fa-abd5-6bfe6d545612
ms.date: 05/21/2018
keywords:
- UsbDeviceCreateTarget ルール (kmdf)
topic_type:
- apiref
api_name:
- UsbDeviceCreateTarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7741d5543a734109611b2354a8821c0351f404e5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918000"
---
# <a name="usbdevicecreatetarget-rule-kmdf"></a>UsbDeviceCreateTarget ルール (kmdf)


**UsbDeviceCreateTarget**ルールでは、現在デバイスコンテキストにある WDFUSBDEVICE オブジェクトがリークしている間に、複数の WDFUSBDEVICE オブジェクトが作成されないことを指定します。

たとえば、システムがリソースを管理しようとしているときに、ドライバーに別のメモリチャンクを割り当てる必要がある場合に、 [*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)イベントコールバック関数を複数回呼び出すことができます。 このような状況では、 [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)イベントのコールバック関数を呼び出して、フレームワークが最初に*Evtdevice hardware*を呼び出した後にメモリリソースをマップ解除します。 次に、デバイスに割り当てられているメモリにドライバーがアクセスできるように、リソースをマップするために、 *Evtdevicepreparehardware*が再度呼び出されます。 このルールは、ドライバーがまずターゲット WDFUSBDEVICE が**NULL**であることを確認し、新しいデバイスを作成して前のハンドルを置き換えるだけではないことを確認します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>UsbDeviceCreateTarget</strong>規則を指定します。</p>
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

[**WdfUsbTargetDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate) 
[ **WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)
 

 





