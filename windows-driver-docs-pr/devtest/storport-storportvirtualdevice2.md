---
title: StorPortVirtualDevice2 ルール (storport)
description: このルールは、HwStorFindAdapter ルーチンが終了したときに、ポート \_ 構成 \_ 情報 (Storport) 構造の virtualdevice フィールドが TRUE に設定されていることを確認します。 このルールは、バーチャル StorPort ミニポートにのみ適用されます。
ms.assetid: CBD1FAD0-9D85-4989-9CCA-00F5698F5383
ms.date: 05/21/2018
keywords:
- StorPortVirtualDevice2 ルール (storport)
topic_type:
- apiref
api_name:
- StorPortVirtualDevice2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85f8700a1593658e47bf70dfc4886c8d9b83a630
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917450"
---
# <a name="storportvirtualdevice2-rule-storport"></a>StorPortVirtualDevice2 ルール (storport)


このルールは、 [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)ルーチンが終了したときに、[**ポート \_ 構成 \_ 情報 (Storport)**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造の**virtualdevice**フィールドが**TRUE**に設定されていることを確認します。 このルールは、バーチャル StorPort ミニポートにのみ適用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>StorPortVirtualDevice2</strong>規則を指定します。</p>
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

 

 





