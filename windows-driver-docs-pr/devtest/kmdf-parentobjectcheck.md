---
title: ParentObjectCheck ルール (kmdf)
description: ParentObjectCheck ルールでは、そのドライバーは、WDF を使用して、親オブジェクトを指定する WdfMemoryCreate を呼び出す必要がありますを指定します\_オブジェクト\_属性の構造体。
ms.assetid: E0597996-9067-40C3-8DE9-1048B2227F07
ms.date: 05/21/2018
keywords:
- ParentObjectCheck ルール (kmdf)
topic_type:
- apiref
api_name:
- ParentObjectCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1c51948ce26f23d1d23bbec7727368e6eec4e2c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392986"
---
# <a name="parentobjectcheck-rule-kmdf"></a>ParentObjectCheck ルール (kmdf)


**ParentObjectCheck**ルールでは、そのドライバーを呼び出す必要がありますを指定します[ **WdfMemoryCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)を使用して親オブジェクトを指定する、 [ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体。 ドライバーが設定されていない場合、フレームワーク、framework メモリ オブジェクトの親オブジェクトは、ドライバーは、framework メモリ オブジェクトを削除しない限り、明示的にありますに残ったままとメモリ ドライバー オブジェクトがアンロードされるまでように、既定の親としてドライバーを設定します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>ParentObjectCheck</strong>ルール。</p>
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

[**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreate)
 

 





