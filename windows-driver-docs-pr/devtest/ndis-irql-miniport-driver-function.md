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
ms.openlocfilehash: 091104219c644dbef52faf10b9aaebe29f4bb9e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573903"
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Miniport_Driver_Function</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**NdisMCreateLog**](https://msdn.microsoft.com/library/windows/hardware/ff563572)
[**NdisMDeregisterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff563574)
[**NdisMDeregisterIoPortRange**](https://msdn.microsoft.com/library/windows/hardware/ff563577) 
 [ **NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578)
[**NdisMFlushLog** ](https://msdn.microsoft.com/library/windows/hardware/ff563584) 
 [ **NdisMFreePort**](https://msdn.microsoft.com/library/windows/hardware/ff563588)
[**NdisMFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563589) 
 [ **NdisMGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff563592)
[**NdisMGetDmaAlignment** ](https://msdn.microsoft.com/library/windows/hardware/ff563593) 
 [**NdisMMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff563613)
[**NdisMPauseComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563628) 
 [ **NdisMQueryAdapterInstanceName**](https://msdn.microsoft.com/library/windows/hardware/ff563630)
[**NdisMReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff563641) 
 [ **NdisMRegisterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff563646)
[**NdisMRegisterIoPortRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563651) 
[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)
[**NdisMRemoveMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff563661) 
 [ **NdisMResetComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563663)
[**NdisMRestartComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563665) 
 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672) 
 [ **NdisMSetupDmaTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff563675)
[**NdisMSleep** ](https://msdn.microsoft.com/library/windows/hardware/ff563677) 
 [ **NdisMUnmapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff563691)
[**NdisMWriteLogData**](https://msdn.microsoft.com/library/windows/hardware/ff563695)








