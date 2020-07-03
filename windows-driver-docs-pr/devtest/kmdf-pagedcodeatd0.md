---
title: PagedCodeAtD0 ルール (kmdf)
description: PagedCodeAtD0 ルールでは、電源コードパス内のコールバック関数内で、ドライバーがコードをページング可能としてマークしてはいけないことを指定します。
ms.assetid: e3e0ee8f-eebe-4855-be35-3d8b153dd09e
ms.date: 05/21/2018
keywords:
- PagedCodeAtD0 ルール (kmdf)
topic_type:
- apiref
api_name:
- PagedCodeAtD0
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35c7bc5a428eb9af9bfa1f2af1197e4861bfbc26
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918238"
---
# <a name="pagedcodeatd0-rule-kmdf"></a>PagedCodeAtD0 ルール (kmdf)


**PagedCodeAtD0**ルールでは、電源コードパス内のコールバック関数内で、ドライバーがコードをページング可能としてマークしてはいけないことを指定します。

関数がページング可能としてマークされ、その後、コードセクションがページアウトされた場合、関数はページフォールトを生成します。これは、コンピューターの高速再開動作に影響を与える可能性があります。 これは、システムドライバーがこのページフォールトを処理できるようになるまで、クライアントドライバーが待機する必要があるためです。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>PagedCodeAtD0</strong>規則を指定します。</p>
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

[**ページング \_ コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
 

 





