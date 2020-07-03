---
title: ForwardedAtBadIrqlAllocate ルール (wdm)
description: ForwardedAtBadIrqlAllocate ルールでは、ドライバーが IRQL ディスパッチレベルで IoCallDriver と PoCallDriver を呼び出す必要があることを指定し \_ ます。ただし、転送される irp メジャー関数コードが、次のいずれかの irp \_ MJ \_ powerirp \_ MJ \_ READIRP \_ MJ \_ writeirp \_ MJ \_ デバイス \_ 制御 lirp \_ MJ \_ 内部 \_ デバイス \_ コントロールです。
ms.assetid: 74BB8358-AE25-4FF8-BBA7-BF108DC2946C
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlAllocate ルール (wdm)
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d679aab97936c40927199d28a16857c073bdf5d0
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916131"
---
# <a name="forwardedatbadirqlallocate-rule-wdm"></a>ForwardedAtBadIrqlAllocate ルール (wdm)


**ForwardedAtBadIrqlAllocate**規則は、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)転送される IRP メジャー関数コードが次のいずれかの場合を除き、ドライバーが IRQL ディスパッチレベルで IoCallDriver と[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を呼び出す必要があることを指定し &lt; \_ ます。

-   [**IRP \_ MJ の \_ 電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)
-   [**IRP \_ MJ の \_ 読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)
-   [**IRP \_ MJ \_ 書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)
-   [**IRP \_ MJ \_ デバイス \_ コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)
-   [**IRP \_ MJ \_ 内部 \_ デバイス \_ コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>ForwardedAtBadIrqlAllocate</strong>規則を指定します。</p>
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

[**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





