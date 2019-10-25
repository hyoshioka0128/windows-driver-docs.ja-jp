---
title: ForwardedAtBadIrqlFsdSync ルール
description: ForwardedAtBadIrqlFsdSync ルールでは、送信される IRP メジャー関数コードが\_MJ\_POWERIRP\_MJ のいずれかである場合を除いて、ドライバーが IRQL ディスパッチ\_レベルで呼び出すことを指定してい\_READIRP\_MJ\_WRITEIRP\_MJ\_デバイス\_コントロール LIRP\_MJ\_内部\_デバイス\_コントロールです。
ms.assetid: 44241FDC-8EC1-4435-B549-80BEEC003C39
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlFsdSync ルール
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlFsdSync
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 309af0b6d38fcfb6b8c99755959da175b1ba02f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839972"
---
# <a name="forwardedatbadirqlfsdsync-rule"></a>ForwardedAtBadIrqlFsdSync ルール


**ForwardedAtBadIrqlFsdSync**規則は、転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)と[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を IRQL&lt;\_ディスパッチすることを指定します。

-   [**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)
-   [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)
-   [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)
-   [**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)
-   [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>ForwardedAtBadIrqlFsdSync</strong>規則を指定します。</p>
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

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)
[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





