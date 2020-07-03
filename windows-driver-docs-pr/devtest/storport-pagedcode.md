---
title: PagedCode ルール (storport)
description: このルールは、ページングされたコードマクロが呼び出されたときに、 \_ ドライバーが IRQL ディスパッチレベルにあることを確認し \_ ます。 \_ページフォールトが発生しないようにするには、IRQL ディスパッチレベルで実行されているすべてのコードが非ページメモリにある必要があります。
ms.assetid: 7FED3FEF-E6E5-4C26-8777-0A4BCCE0E1EE
ms.date: 05/21/2018
keywords:
- PagedCode ルール (storport)
topic_type:
- apiref
api_name:
- PagedCode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: daad3c8547dfc9686e558a9d17350b02b981d9a1
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916731"
---
# <a name="pagedcode-rule-storport"></a>PagedCode ルール (storport)


このルールは、ページングされた[** \_ コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)マクロが呼び出されたときに、ドライバーが**IRQL &lt; ディスパッチ \_ レベル**にあることを確認します。 ページフォールトが発生しないようにするには、 **IRQL &gt; = ディスパッチ \_ レベル**で実行されているすべてのコードが非ページメモリにある必要があります。

**ドライバーモデル: Storport**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>PagedCode</strong>規則を指定します。</p>
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
 

 





