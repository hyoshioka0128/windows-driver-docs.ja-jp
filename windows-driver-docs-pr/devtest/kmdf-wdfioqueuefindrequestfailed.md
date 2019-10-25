---
title: WdfIoQueueFindRequestFailed ルール (kmdf)
description: WdfIoQueueFindRequestFailed 規則は、WdfIoQueueRetrieveFoundRequest または Wdfobject逆参照は、wdfioqueuefindrequestfailed Failed が正常終了したときにのみ呼び出す必要があることを指定します。
ms.assetid: 9D211A0A-36CB-4083-B379-EE1C34A7B50F
ms.date: 05/21/2018
keywords:
- WdfIoQueueFindRequestFailed ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfIoQueueFindRequestFailed
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76139a1f691f5a7054692a389908cbfd6f00d463
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839431"
---
# <a name="wdfioqueuefindrequestfailed-rule-kmdf"></a>WdfIoQueueFindRequestFailed ルール (kmdf)


**Wdfioqueuefindrequestfailed**規則は、 [**WdfIoQueueRetrieveFoundRequest**](kmdf-wdfioqueueretrievefoundrequest.md)または[**Wdfobject逆参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)は、 **WDFIOQUEUEFINDREQUESTFAILED failed**が正常終了したときにのみ呼び出す必要があることを指定します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Wdfioqueuefindrequestfailed</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
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
[**wdfobject逆参照**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
 

 





