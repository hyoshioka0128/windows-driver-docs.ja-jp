---
title: CtlDeviceFinishInitDeviceAdd ルール (kmdf)
description: CtlDeviceFinishInitDeviceAdd ルールは、ドライバーが EvtDriverDeviceAdd コールバック関数にコントロールデバイスオブジェクトを作成する場合、デバイスが作成された後、および EvtDriverDeviceAdd コールバック関数から終了する前に、Wdfcontrolfinish を呼び出す必要があることを指定します。 このルールは、PnP 以外のドライバーには適用されません。
ms.assetid: 162a0013-1215-487c-af72-05e75ef0bdbd
ms.date: 05/21/2018
keywords:
- CtlDeviceFinishInitDeviceAdd ルール (kmdf)
topic_type:
- apiref
api_name:
- CtlDeviceFinishInitDeviceAdd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c65031df073cc40cf3dd2597a80d6281e50aae4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916508"
---
# <a name="ctldevicefinishinitdeviceadd-rule-kmdf"></a>CtlDeviceFinishInitDeviceAdd ルール (kmdf)


**CtlDeviceFinishInitDeviceAdd**ルールは、ドライバーが[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数にコントロールデバイスオブジェクトを作成する場合、デバイスが作成された後、および**evtdriverdeviceadd**コールバック関数から終了する前に、 [**wdfcontrolfinish**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)を呼び出す必要があることを指定します。 このルールは、PnP 以外のドライバーには適用されません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>CtlDeviceFinishInitDeviceAdd</strong>規則を指定します。</p>
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
[**Wdfcontrolfinish の初期化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing) 
[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 
[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)
 

 





