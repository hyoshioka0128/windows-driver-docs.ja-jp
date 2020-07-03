---
title: WmiComplete ルール (wdm)
description: WmiComplete ルールは、WMI のマイナー IRP を処理するときに、ドライバーが IoCompleteRequest を呼び出してから、DispatchSystemControl ルーチンから制御を戻すことを指定します。
ms.assetid: 3908da96-beb1-4651-b41b-06f849b72000
ms.date: 05/21/2018
keywords:
- WmiComplete ルール (wdm)
topic_type:
- apiref
api_name:
- WmiComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f224b1693a8a740cff0f6ed86d2f0f2eacac293
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917404"
---
# <a name="wmicomplete-rule-wdm"></a>WmiComplete ルール (wdm)


**WmiComplete**ルールは、 [**WMI のマイナー IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)を処理するときに、ドライバーが[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出してから、 [**DispatchSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから制御を戻すことを指定します。

*Wmi MINOR irp*は、wmi マイナー関数コードを含む[**irp \_ MJ \_ システム \_ 制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求です。

WMI のマイナー Irp の処理の詳細については、「 [**WDM ドライバーの Wmi 要件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers)」、「 [**wmi 要求の処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」、「 [**Windows Management Instrumentation ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」、および「 [**wmi ライブラリサポートルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

WMI データプロバイダーとして登録されていないドライバーは、次の下位のドライバーに WMI 要求を転送する必要があります。 このアクションを確認するには、"参照[**先**](wdm-wmiforward.md)" ルールを使用します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>WmiComplete</strong>規則を指定します。</p>
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

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)関連項目
--------

参照[**先**](wdm-wmiforward.md) 
[**WDM ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-requirements-for-wdm-drivers) 
 の WMI 要件[**WMI 要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests) 
 の処理[**WMI ライブラリのサポートルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
 

 





