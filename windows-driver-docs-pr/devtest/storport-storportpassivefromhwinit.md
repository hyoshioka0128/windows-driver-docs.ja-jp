---
title: Storport"Vefromhwinit ルール (storport)"
description: Hw 初期化エントリポイントを HW アダプターコントロールのエントリポイントから直接呼び出すことができる場合、Storport ドライバーの HW 初期化エントリポイント内で Storportenableの Veinitialization を呼び出すことはできません。
ms.assetid: F6AD52D5-4964-4406-AF5F-2820273D337C
ms.date: 05/21/2018
keywords:
- Storport"Vefromhwinit ルール (storport)"
topic_type:
- apiref
api_name:
- StorPortPassiveFromHwInit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07c3bf0590e392c07d4fb785ff094585cbda638a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917167"
---
# <a name="storportpassivefromhwinit-rule-storport"></a>Storport"Vefromhwinit ルール (storport)"


Hw 初期化エントリポイントを HW アダプターコントロールのエントリポイントから直接呼び出すことができる場合、Storport ドライバーの HW 初期化エントリポイント内で**Storportenableの Veinitialization**を呼び出すことはできません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバーの検証ツール</a>を実行し、 <strong>storportの</strong>"規則" を指定します。</p>
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

[**Storportenableveinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportenablepassiveinitialization)
 

 





