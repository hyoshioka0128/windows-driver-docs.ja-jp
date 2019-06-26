---
title: IrqlKeWaitForMultipleObjects ルール (wdm)
description: IrqlKeWaitForMultipleObjects ルールでは、タイムアウト パラメーターに基づいて適切な IRQL で KeWaitForMultipleObjects ルーチンの呼び出し元を実行する必要がありますを指定します。
ms.assetid: FC3E3544-95FB-4283-B030-66D74D0F7848
ms.date: 05/21/2018
keywords:
- IrqlKeWaitForMultipleObjects ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeWaitForMultipleObjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3035d840ba0160fa54860e46058345be5641ff3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393848"
---
# <a name="irqlkewaitformultipleobjects-rule-wdm"></a>IrqlKeWaitForMultipleObjects ルール (wdm)


**IrqlKeWaitForMultipleObjects**ことを指定するルールの呼び出し元、 [ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects) に基づいて適切なIRQLでルーチンを実行する必要があります*タイムアウト*パラメーター。

呼び出し元**IrqlKeWaitForMultipleObjects** IRQL でルーチンを実行できる&lt;= ディスパッチ\_レベル、を除き、次の状況で。

-   場合*タイムアウト* &lt; &gt; 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects) IRQL でルーチンを実行する必要があります&lt;APCを=\_レベルです。
-   場合*タイムアウト*! = NULL と\**タイムアウト*= 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)ルーチンを実行する必要がありますIRQL = ディスパッチ\_レベル。

-   場合*タイムアウト* = **NULL**、または\**タイムアウト*! = 0 の場合、呼び出し元の[ **KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)ルーチンは、IRQL で実行する必要があります&lt;APC を =\_レベル。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>IrqlKeWaitForMultipleObjects</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)
 

 





