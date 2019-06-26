---
title: StorPortPassiveFromHwInit ルール (storport)
description: StorPortEnablePassiveInitialization 呼び出さないで HW 初期化のエントリ ポイント内で Storport ドライバーの場合は、ハードウェアの初期化のエントリ ポイントをハードウェア アダプターのコントロールのエントリ ポイントから直接呼び出すことができます。
ms.assetid: F6AD52D5-4964-4406-AF5F-2820273D337C
ms.date: 05/21/2018
keywords:
- StorPortPassiveFromHwInit ルール (storport)
topic_type:
- apiref
api_name:
- StorPortPassiveFromHwInit
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6496c221895955971a3976c50809fd9c3b56b9a7
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391828"
---
# <a name="storportpassivefromhwinit-rule-storport"></a>StorPortPassiveFromHwInit ルール (storport)


**StorPortEnablePassiveInitialization**呼び出すことはできません HW 初期化のエントリ ポイント内で Storport ドライバーの場合は、ハードウェアの初期化のエントリ ポイントをハードウェア アダプターのコントロールのエントリ ポイントから直接呼び出すことができます。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortPassiveFromHwInit</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortEnablePassiveInitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportenablepassiveinitialization)
 

 





