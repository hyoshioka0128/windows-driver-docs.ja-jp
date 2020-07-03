---
title: Irql \_ フィルター \_ ドライバー \_ 関数規則 (ndis)
description: Irql \_ フィルター \_ ドライバー関数の規則は、 \_ フィルタードライバーの NDIS 関数を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: 1dd45962-151b-472c-88a6-6042ecb7491c
ms.date: 05/21/2018
keywords:
- Irql_Filter_Driver_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_Filter_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d41469391daaeb3862665b538d55c2c2402cec2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917780"
---
# <a name="irql_filter_driver_function-rule-ndis"></a>Irql \_ フィルター \_ ドライバー \_ 関数規則 (ndis)


Irql \_ フィルター \_ ドライバー関数の規則は、 \_ フィルタードライバーの NDIS 関数を正しい Irql レベルで呼び出す必要があることを指定します。

フィルタードライバー用の NDIS 関数は次のとおりです。

**NdisFRegisterFilterDriver** 
**NdisFDeregisterFilterDriver** 
**NdisFSetAttributes** 
**NdisFRestartFilter** 
**NdisFRestartComplete** 
**NdisFPauseComplete** 
**NdisFSendNetBufferLists** 
**NdisFReturnNetBufferLists** 
**NdisFSendNetBufferListsComplete** 
**NdisFCancelSendNetBufferLists** 
**NdisFIndicateReceiveNetBufferLists** 
**NdisFNetPnPEvent** 
**NdisFDevicePnPEventNotify** 
**NdisEnumerateFilterModules**

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Filter_Driver_Function</strong>規則を指定します。</p>
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

[**NdisEnumerateFilterModules**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisenumeratefiltermodules) 
[**NdisFCancelSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfcancelsendnetbufferlists) 
[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver) 
[**NdisFDevicePnPEventNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdevicepnpeventnotify) 
[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists) 
[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) 
[**NdisFPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfpausecomplete) 
[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver) 
[**NdisFRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartcomplete) 
[**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter) 
[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists) 
[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) 
[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete) 
[**NdisFSetAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsetattributes)








