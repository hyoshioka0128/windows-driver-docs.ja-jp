---
title: IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)
description: IoSetCompletionRoutineExCheckDeviceObject ルールでは、現在のデバイスオブジェクトが IoSetCompletionRoutineEx に渡されず、それより小さいデバイスオブジェクトがである場合、完了ルーチンが実行されていなくても、現在のデバイスオブジェクトがアンロードされる可能性があることを指定します。
ms.assetid: 037E4CED-FBC7-480F-B81F-561396A217C6
ms.date: 05/21/2018
keywords:
- IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)
topic_type:
- apiref
api_name:
- IoSetCompletionRoutineExCheckDeviceObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be1d7cee0f430b2eaf32180a871483a730d2cf28
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917534"
---
# <a name="iosetcompletionroutineexcheckdeviceobject-rule-wdm"></a>IoSetCompletionRoutineExCheckDeviceObject ルール (wdm)


**IoSetCompletionRoutineExCheckDeviceObject**ルールでは、現在のデバイスオブジェクトが[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)に渡されず、それより小さいデバイスオブジェクトがである場合、完了ルーチンが実行されていなくても、現在のデバイスオブジェクトがアンロードされる可能性があることを指定します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IoSetCompletionRoutineExCheckDeviceObject</strong>規則を指定します。</p>
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

[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)
 

 





