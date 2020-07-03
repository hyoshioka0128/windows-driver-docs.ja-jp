---
title: WdfIoQueueRetrieveFoundRequest ルール (kmdf)
description: WdfIoQueueRetrieveFoundRequest ルールでは、WdfIoQueueRetrieveFoundRequest メソッドが呼び出されるように指定します。これは、WdfIoQueueFindRequest が呼び出され、STATUS SUCCESS が返され、 \_ 同じ要求に対して Wdfobject逆参照が呼び出されないことを示します。
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
ms.openlocfilehash: f52e8aee39edd7ddb77ed9cf05998d2c160fe23f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917968"
---
# <a name="wdfioqueueretrievefoundrequest-rule-kmdf"></a>WdfIoQueueRetrieveFoundRequest ルール (kmdf)


**WdfIoQueueRetrieveFoundRequest**ルールでは、 [**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)メソッドが呼び出されるように指定します。これは、 [**Wdfioqueuefindrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)が呼び出され、STATUS SUCCESS が返され、 \_ 同じ要求に対して[**wdfobject逆参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)が呼び出されないことを示します。

[**Wdfioqueuefindrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)が STATUS SUCCESS を返した場合 \_ 、出力要求オブジェクトの参照カウントをインクリメントします。この要求ハンドルの使用が完了したら、ドライバーは[**wdfobject逆参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)を呼び出す必要があります。

**ドライバーモデル: KMDF**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>WdfIoQueueRetrieveFoundRequest</strong>規則を指定します。</p>
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

[**Wdfioqueuefindrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest) 
[**WdfIoQueueRetrieveFoundRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest) 
[**Wdfobjectdereference 参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
 

 





