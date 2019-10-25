---
title: IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)
description: IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルールでは、IoReleaseRemoveLockAndWait を irp\_\_MJ の外部で呼び出すことを指定します。 IRP\_は、PnP ドライバー用の\_デバイスを削除\_ます。
ms.assetid: 5787B14D-1793-4B39-A569-9A1308257A26
ms.date: 05/21/2018
keywords:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)
topic_type:
- apiref
api_name:
- IoReleaseRemoveLockAndWaitOutsideRemoveDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 67f8cee5228ee44d62455c79ce98690b105b42a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839207"
---
# <a name="ioreleaseremovelockandwaitoutsideremovedevice-rule-wdm"></a>IoReleaseRemoveLockAndWaitOutsideRemoveDevice ルール (wdm)


**IoReleaseRemoveLockAndWaitOutsideRemoveDevice**ルールでは、 [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を irp\_\_MJ の外部で呼び出すことを指定します。 Irp\_は、pnp ドライバー用の\_デバイスを削除\_ます。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong>規則を指定します。</p>
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

[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)関連項目
--------

[削除ロックの使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-remove-locks)
 

 





