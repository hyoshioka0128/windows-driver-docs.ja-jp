---
title: NdisFDeregisterFilterDriver rule (ndis)
description: フィルタードライバーは、FilterDriverUnload ルーチンから NdisFDeregisterFilterDriver を呼び出す必要があります。
ms.assetid: 24EEB6F6-EEBC-482B-BCAE-DE43277DE899
ms.date: 05/21/2018
keywords:
- NdisFDeregisterFilterDriver rule (ndis)
topic_type:
- apiref
api_name:
- NdisFDeregisterFilterDriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8ff371a7bb2414e09b838f1aecf16d475538404
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917065"
---
# <a name="ndisfderegisterfilterdriver-rule-ndis"></a>NdisFDeregisterFilterDriver rule (ndis)


フィルタードライバーは、 [**Filterdriverunload**](https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver)ルーチンから[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)を呼び出す必要があります。

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>NdisFDeregisterFilterDriver</strong>規則を指定します。</p>
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

[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver) 
[ **NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)
 

 





