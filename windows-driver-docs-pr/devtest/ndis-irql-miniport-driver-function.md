---
title: Irql \_ ミニポート \_ ドライバー \_ 機能ルール (ndis)
description: Irql \_ ミニポート \_ ドライバー \_ の関数ルールでは、ミニポートドライバーの NDIS 関数を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: b82627db-63bd-413f-9d7f-dbb611cf2c50
ms.date: 05/21/2018
keywords:
- Irql_Miniport_Driver_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_Miniport_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08d868dd7af043cb735eae8d1fe440bf4d3cd86e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916540"
---
# <a name="irql_miniport_driver_function-rule-ndis"></a>Irql \_ ミニポート \_ ドライバー \_ 機能ルール (ndis)


Irql \_ ミニポート \_ ドライバー \_ の関数ルールでは、ミニポートドライバーの NDIS 関数を正しい Irql レベルで呼び出す必要があることを指定します。

このルールは、NDIS ミニポートドライバーのログ、NDIS ポート、および NDIS DMA インターフェイスの機能を検証します。

**NdisMCreateLog** 
**NdisMDeregisterDmaChannel** 
**NdisMDeregisterIoPortRange** 
**NdisMDeregisterMiniportDriver** 
**NdisMFlushLog** 
**NdisMFreePort** 
**NdisMFreeSharedMemory** 
**NdisMGetDeviceProperty** 
**NdisMGetDmaAlignment** 
**NdisMMapIoSpace** 
**NdisMPauseComplete** 
**NdisMQueryAdapterInstanceName** 
**NdisMReadDmaCounter** 
**NdisMRegisterDmaChannel** 
**NdisMRegisterIoPortRange** 
**NdisMRegisterMiniportDriver** 
**NdisMRemoveMiniport** 
**NdisMResetComplete** 
**NdisMRestartComplete** 
**NdisMSetMiniportAttributes** 
**NdisMSetupDmaTransfer** 
**NdisMSleep** 
**NdisMUnmapIoSpace** 
**NdisMUpdateSharedMemory** 
**NdisMWriteLogData**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Miniport_Driver_Function</strong>規則を指定します。</p>
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

[**NdisMCreateLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcreatelog) 
[**NdisMDeregisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterdmachannel) 
[**NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterioportrange) 
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 
[**NdisMFlushLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismflushlog) 
[**NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreeport) 
[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory) 
[**NdisMGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdeviceproperty) 
[**NdisMGetDmaAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetdmaalignment) 
[**NdisMMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismmapiospace) 
[**NdisMPauseComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismpausecomplete) 
[**NdisMQueryAdapterInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryadapterinstancename) 
[**NdisMReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreaddmacounter) 
[**NdisMRegisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterdmachannel) 
[**NdisMRegisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterioportrange) 
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 
[**NdisMRemoveMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport) 
[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete) 
[**NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismrestartcomplete) 
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 
[**NdisMSetupDmaTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetupdmatransfer) 
[**NdisMSleep**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsleep) 
[**NdisMUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismunmapiospace) 
[**NdisMWriteLogData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismwritelogdata)








