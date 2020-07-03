---
title: Wmi 転送ルール (wdm)
description: "\"WMI 転送\" 規則は、転送が必要な場合に、ドライバーが WMI のマイナー Irp を転送する必要があることを指定します。"
ms.assetid: c62f37d2-ebd5-4705-9590-d1bf17137802
ms.date: 05/21/2018
keywords:
- Wmi 転送ルール (wdm)
topic_type:
- apiref
api_name:
- WmiForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7580e7a01bfea79e01ae666d2a70d2153e167cf3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917402"
---
# <a name="wmiforward-rule-wdm"></a>Wmi 転送ルール (wdm)


"Wmi**転送**" 規則は、転送が必要な場合に、ドライバーが[**WMI のマイナー irp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)を転送する必要があることを指定します。

具体的には、ドライバーが呼び出し元*のパラメーターの*値が**irpdisposition**の場合、ドライバーは[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)または[**POCALLDRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)を[**呼び出して、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) IRP を転送してからディスパッチルーチンから戻る必要があります。

このルールは、バスドライバには適用されません。

*Wmi MINOR irp*は、wmi マイナー関数コードを含む[**irp \_ MJ \_ システム \_ 制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求です。

WMI のマイナー Irp の処理の詳細については、「 [**WDM ドライバーの Wmi 要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)」、「 [**wmi 要求の処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」、「 [**Windows Management Instrumentation ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」、および「 [**wmi ライブラリサポートルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的なドライバーの検証ツール</a>を実行<strong>し、[設定] 規則を</strong>指定します。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)関連項目
--------

[**WDM ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers) 
 の WMI 要件[**WMI 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests) 
 の処理[**WMI ライブラリのサポートルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
 

 





