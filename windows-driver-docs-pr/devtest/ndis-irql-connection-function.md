---
title: Irql\_接続\_関数規則 (ndis)
description: Irql\_接続\_機能ルールでは、プロトコルドライバーの NDIS 接続関数を正しい IRQL レベルで呼び出す必要があることを指定します。
ms.assetid: 9721cb8a-ac70-4f2b-8bbd-809dc06548dc
ms.date: 05/21/2018
keywords:
- Irql_Connection_Function rule (ndis)
topic_type:
- apiref
api_name:
- Irql_Connection_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e47b88319e890892c262e616a3d0c5a36f9a018
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840117"
---
# <a name="irql_connection_function-rule-ndis"></a>Irql\_接続\_関数規則 (ndis)


**Irql\_接続\_機能**ルールでは、プロトコルドライバーの NDIS 接続関数を正しい Irql レベルで呼び出す必要があることを指定します。

このルールは、次の NDIS 関数を検証します。

**NdisCoAssignInstanceNam**
**NdisCoCreateVc**
**NdisCoDeleteVc**
**NdisCoGetTapiCallId**
**NdisCoOidRequest**
**NdisCoOidRequestComplete**
**NdisCoSendNetBufferLists**

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Connection_Function</strong>規則を指定します。</p>
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

[**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)
[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)
[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)
[**NdisCoGetTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscogettapicallid)
[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)
[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)
[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)








