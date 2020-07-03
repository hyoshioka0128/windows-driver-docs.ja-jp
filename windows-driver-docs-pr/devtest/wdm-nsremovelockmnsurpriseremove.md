---
title: NsRemoveLockMnSurpriseRemove ルール (wdm)
description: NsRemoveLockMnSurpriseRemove ルールは、 \_ \_ \_ \_ minorfunction irp の削除を使用して、irp MJ PNP 要求を処理するときに、ドライバーがサポートされていないステータスを返さないことを確認し \_ \_ \_ ます。 このルールは、FDO および FIDO ドライバーにのみ適用されます。
ms.assetid: A7F444B1-615F-4DE2-B1AF-C179C5103DD9
ms.date: 05/21/2018
keywords:
- NsRemoveLockMnSurpriseRemove ルール (wdm)
topic_type:
- apiref
api_name:
- NsRemoveLockMnSurpriseRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfb7be404e64d5c68290094e98bc92a9e12937af
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916955"
---
# <a name="nsremovelockmnsurpriseremove-rule-wdm"></a>NsRemoveLockMnSurpriseRemove ルール (wdm)


**NsRemoveLockMnSurpriseRemove**ルールは、 \_ \_ \_ \_ minorfunction irp の削除を使用して、irp MJ PNP 要求を処理するときに、ドライバーがサポートされていない \_ ステータス \_ \_ を返さないことを確認します。 このルールは、FDO および FIDO ドライバーにのみ適用されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>NsRemoveLockMnSurpriseRemove</strong>規則を指定します。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
 

 





