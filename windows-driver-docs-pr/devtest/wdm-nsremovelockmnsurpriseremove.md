---
title: NsRemoveLockMnSurpriseRemove ルール (wdm)
description: NsRemoveLockMnSurpriseRemove ルールは、ドライバーが状態を返さないことを確認します\_いない\_IRP の処理時にサポートされている\_MJ\_PNP IRP minorFunction 要求\_MN\_ 。SUPRISE\_削除します。 このルールは、FDO および FIDO ドライバーのみに適用されます。
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
ms.openlocfilehash: fa90cdb8a938e75f8ef32b26f6338a64d0f2b179
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393724"
---
# <a name="nsremovelockmnsurpriseremove-rule-wdm"></a>NsRemoveLockMnSurpriseRemove ルール (wdm)


**NsRemoveLockMnSurpriseRemove**ルールは、ドライバーが状態を返さないことを確認します\_いない\_IRP の処理時にサポートされている\_MJ\_PNP IRP minorFunction と要求。\_MN\_SUPRISE\_削除します。 このルールは、FDO および FIDO ドライバーのみに適用されます。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>NsRemoveLockMnSurpriseRemove</strong>ルール。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)
 

 





