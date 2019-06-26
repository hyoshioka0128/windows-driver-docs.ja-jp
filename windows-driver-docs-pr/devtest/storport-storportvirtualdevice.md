---
title: StorPortVirtualDevice ルール (storport)
description: このルールでは、ことを確認 HwStorFindAdapter ルーチンからの終了時、ポート VirtualDevice フィールドに\_構成\_情報 (Storport) 構造体を FALSE に設定されています。 ルールは、物理 StorPort ミニポートにのみ適用されます。
ms.assetid: AC0550F8-117B-4942-8F8B-E7FE71D5AF71
ms.date: 05/21/2018
keywords:
- StorPortVirtualDevice ルール (storport)
topic_type:
- apiref
api_name:
- StorPortVirtualDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 337b6c30a7a2fa08fdfb88ffaea1ed3e9dc884e5
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391790"
---
# <a name="storportvirtualdevice-rule-storport"></a>StorPortVirtualDevice ルール (storport)


終了時にこの規則を確認、 [ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter) 、ルーチン、 **VirtualDevice**フィールドに、 [**ポート\_構成\_情報 (Storport)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造に設定されている**FALSE**します。 ルールは、物理 StorPort ミニポートにのみ適用されます。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortVirtualDevice</strong>ルール。</p>
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

 

 





