---
title: Irql\_ミニポート\_ドライバー\_関数ルール (ndis)
description: Irql\_ミニポート\_ドライバー\_関数の規則は、適切な IRQL レベルでのミニポート ドライバーの NDIS 関数を呼び出す必要がありますを指定します。
ms.assetid: b82627db-63bd-413f-9d7f-dbb611cf2c50
ms.date: 05/21/2018
keywords:
- Irql_Miniport_Driver_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Miniport_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35acfc83ebe3ba146e3bcabab1c876888c6b8636
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392314"
---
# <a name="irqlminiportdriverfunction-rule-ndis"></a>Irql\_ミニポート\_ドライバー\_関数ルール (ndis)


Irql\_ミニポート\_ドライバー\_関数の規則は、適切な IRQL レベルでのミニポート ドライバーの NDIS 関数を呼び出す必要がありますを指定します。

このルールは、NDIS ミニポート ドライバーのログ記録、NDIS ポート、および NDIS DMA インターフェイスの機能を確認します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>Irql_Miniport_Driver_Function</strong>ルール。</p>
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

[**NdisMCreateLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcreatelog)
[**NdisMDeregisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterdmachannel)
[**NdisMDeregisterIoPortRange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterioportrange) 
 [ **NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)
[**NdisMFlushLog** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismflushlog) 
 [ **NdisMFreePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)
[**NdisMFreeSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory) 
 [ **NdisMGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetdeviceproperty)
[**NdisMGetDmaAlignment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetdmaalignment) 
 [**NdisMMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismmapiospace)
[**NdisMPauseComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismpausecomplete) 
 [ **NdisMQueryAdapterInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueryadapterinstancename)
[**NdisMReadDmaCounter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismreaddmacounter) 
 [ **NdisMRegisterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterdmachannel)
[**NdisMRegisterIoPortRange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterioportrange) 
[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)
[**NdisMRemoveMiniport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismremoveminiport) 
 [ **NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismresetcomplete)
[**NdisMRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismrestartcomplete) 
 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes) 
 [ **NdisMSetupDmaTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetupdmatransfer)
[**NdisMSleep** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsleep) 
 [ **NdisMUnmapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismunmapiospace)
[**NdisMWriteLogData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismwritelogdata)








