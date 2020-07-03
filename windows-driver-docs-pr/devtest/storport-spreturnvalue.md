---
title: SpReturnValue 規則 (storport)
description: このルールは、HwStorFindAdapter と VirtualHwStorFindAdapter のドライバーの実装が有効な状態を返すことを確認します。 有効な状態は、次のいずれかの SP の \_ 戻り値が \_ 見つかりました、sp を \_ 返す \_ エラー、sp を \_ 返す \_ 無効な \_ 構成、または sp の \_ 戻り値が \_ 見つかりません \_ 。
ms.assetid: 4F9E0FE3-4B1B-4C06-9DA0-8307C43E0DBA
ms.date: 05/21/2018
keywords:
- SpReturnValue 規則 (storport)
topic_type:
- apiref
api_name:
- SpReturnValue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b76fbb380a2f2e671e9df9d566d3d0d1a326fbf
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916689"
---
# <a name="spreturnvalue-rule-storport"></a>SpReturnValue 規則 (storport)


このルールは、 [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)と[**VirtualHwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)のドライバーの実装が有効な状態を返すことを確認します。 有効な状態は次のいずれかです: **sp の \_ 戻り \_ **値、sp の** \_ 戻り \_ **値、Sp が無効な** \_ \_ \_ 構成**、または**sp の \_ 戻り値が \_ \_ 見つかりません**。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>spreturnvalue</strong>規則を指定します。</p>
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

 

 





