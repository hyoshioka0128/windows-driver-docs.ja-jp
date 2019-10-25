---
title: ControlDeviceDeleted ルール (kmdf)
description: 制御 Devicedeleted ルールは、PnP ドライバーがコントロールデバイスオブジェクトを作成する場合、ドライバーは、ドライバーがアンロードされる前に、いずれかのクリーンアップコールバック関数でコントロールデバイスオブジェクトを削除する必要があることを指定します。
ms.assetid: 869f1c1c-8a9f-4e0b-bcbb-386e93663567
ms.date: 05/21/2018
keywords:
- ControlDeviceDeleted ルール (kmdf)
topic_type:
- apiref
api_name:
- ControlDeviceDeleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 98237d89cbbef4e4d9fb9a2bb309af8181a7fa1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839527"
---
# <a name="controldevicedeleted-rule-kmdf"></a>ControlDeviceDeleted ルール (kmdf)


制御 Devicedeleted ルールは、PnP ドライバーがコントロールデバイスオブジェクトを作成する場合、ドライバーは、ドライバーがアンロードされる前に、いずれかのクリーンアップコールバック関数でコントロールデバイスオブジェクトを削除する必要があることを指定します。

FDO またはフィルタードライバーがコントロールデバイスオブジェクトの[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す場合、ドライバーは、WDFDEVICE オブジェクトのドライバーのクリーンアップコールバック関数からコントロールデバイスオブジェクトに対して[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出す必要があります。破棄コールバックWDFDEVICE オブジェクトの関数、または[*Evtdeviceselfmanagediocleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)イベントコールバック関数。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>controldevicedeleted</strong>ルールを指定します。</p>
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
[ **wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)
 

 





