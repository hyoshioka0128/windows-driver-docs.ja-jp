---
title: InitFreeDeviceCreateType2 ルール (kmdf)
description: InitFreeDeviceCreateType2 規則は、WdfDeviceInitFree を呼び出した後、ドライバーが WdfDeviceCreate を呼び出すことができないことを指定します。
ms.assetid: 43defbbb-ab5e-4c3e-bb9d-fdcbe203c617
ms.date: 05/21/2018
keywords:
- InitFreeDeviceCreateType2 ルール (kmdf)
topic_type:
- apiref
api_name:
- InitFreeDeviceCreateType2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1fe9482a65f8b6432bb0ede1c3fc740e2b5e5e89
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917002"
---
# <a name="initfreedevicecreatetype2-rule-kmdf"></a>InitFreeDeviceCreateType2 ルール (kmdf)


InitFreeDeviceCreateType2 規則は、 [**Wdfdeviceinitfree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)を呼び出した後、ドライバーが[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことができないことを指定します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>InitFreeDeviceCreateType2</strong>規則を指定します。</p>
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

[**Wdfcontroldeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate) 
[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 
[**Wdfdeviceinitfree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)関連項目
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md) 
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md) 
[**InitFreeDeviceCreateType4**](kmdf-initfreedevicecreatetype4.md) 
[**PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md) 
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
[**PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md) 
[**InitFreeNull**](kmdf-initfreenull.md)
 

 





