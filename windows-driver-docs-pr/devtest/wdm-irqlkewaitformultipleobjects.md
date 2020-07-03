---
title: IrqlKeWaitForMultipleObjects ルール (wdm)
description: IrqlKeWaitForMultipleObjects 規則は、KeWaitForMultipleObjects ルーチンの呼び出し元が、Timeout パラメーターに基づいて適切な IRQL で実行されている必要があることを指定します。
ms.assetid: FC3E3544-95FB-4283-B030-66D74D0F7848
ms.date: 05/21/2018
keywords:
- IrqlKeWaitForMultipleObjects ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeWaitForMultipleObjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ef99e071d1a0e08ae03e2c67e73752ab6fc6bc6
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917884"
---
# <a name="irqlkewaitformultipleobjects-rule-wdm"></a>IrqlKeWaitForMultipleObjects ルール (wdm)


**IrqlKeWaitForMultipleObjects**規則は、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)ルーチンの呼び出し元が、 *Timeout*パラメーターに基づいて適切な IRQL で実行されている必要があることを指定します。

**IrqlKeWaitForMultipleObjects**ルーチンの呼び出し元は &lt; \_ 、次の場合を除き、IRQL = ディスパッチレベルで実行できます。

-   *Timeout* 0 の場合 &lt; &gt; 、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)ルーチンの呼び出し元は、IRQL = APC レベルで実行されている必要があり &lt; \_ ます。
-   *Timeout* ! = NULL および \* *timeout* = 0 の場合、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)ルーチンの呼び出し元は、IRQL = ディスパッチレベルで実行されている必要があり \_ ます。

-   *Timeout*  =  **NULL**または \* *timeout* ! = 0 の場合、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)ルーチンの呼び出し元は、IRQL = APC レベルで実行する必要があり &lt; \_ ます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlKeWaitForMultipleObjects</strong>規則を指定します。</p>
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

[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)
 

 





