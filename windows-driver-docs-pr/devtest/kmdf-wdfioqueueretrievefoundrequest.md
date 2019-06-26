---
title: WdfIoQueueRetrieveFoundRequest ルール (kmdf)
description: WdfIoQueueRetrieveFoundRequest ルールでは、WdfIoQueueFindRequest が呼び出され、状態が返された後のみに、WdfIoQueueRetrieveFoundRequest メソッドを呼び出すことを指定します\_同じ要求に成功した場合とない WdfObjectDereference と呼びます。
ms.assetid: CF545174-5E6D-429B-AC6D-BA7A84852FC1
ms.date: 05/21/2018
keywords:
- WdfIoQueueRetrieveFoundRequest ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfIoQueueRetrieveFoundRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 010e64bd346ff3521d265680b30f9fef6d575bb2
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392814"
---
# <a name="wdfioqueueretrievefoundrequest-rule-kmdf"></a>WdfIoQueueRetrieveFoundRequest ルール (kmdf)


**WdfIoQueueRetrieveFoundRequest**ルールを指定する[ **WdfIoQueueRetrieveFoundRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)後のみメソッドが呼び出された[ **WdfIoQueueFindRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)呼び出され、状態が返されました\_成功と no [ **WdfObjectDereference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)が同じ要求で呼び出されます。

場合[ **WdfIoQueueFindRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)ステータスを返します\_出力要求の参照カウントをインクリメント成功オブジェクト、ドライバーを呼び出す必要があります[ **WdfObjectDereference** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)終了後にこの要求ハンドルを使用します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WdfIoQueueRetrieveFoundRequest</strong>ルール。</p>
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

[**WdfIoQueueFindRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)
[**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)
[**WdfObjectDereference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
 

 





