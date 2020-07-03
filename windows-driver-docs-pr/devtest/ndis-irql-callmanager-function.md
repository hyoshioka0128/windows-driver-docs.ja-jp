---
title: Irql \_ callmanager \_ 関数ルール (ndis)
description: Irql \_ callmanager 関数ルールでは、 \_ Ndis CALLMANAGER の ndis 関数を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: 3e026fb0-8c5f-40cc-affb-3b35f17f40f7
ms.date: 05/21/2018
keywords:
- Irql_CallManager_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_CallManager_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a5c275df697433842aa4f782326979a87331f6d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917796"
---
# <a name="irql_callmanager_function-rule-ndis"></a>Irql \_ callmanager \_ 関数ルール (ndis)


**Irql \_ callmanager \_ 関数**ルールでは、NDIS callmanager の NDIS 関数を正しい Irql レベルで呼び出す必要があることを指定します。

このルールは、次の NDIS 関数を検証します。

**NdisCmActivateVc** 
**NdisCmAddPartyComplete** 
**NdisCmCloseAddressFamilyComplete** 
**NdisCmCloseCallComplete** 
**NdisCmDeactivateVc** 
**NdisCmDeregisterSapComplete** 
**NdisCmDispatchCallConnected** 
**NdisCmDispatchIncomingCall** 
**NdisCmDispatchIncomingCallQoSChange** 
**NdisCmDispatchIncomingCloseCall** 
**NdisCmDispatchIncomingDropParty** 
**NdisCmDropPartyComplete** 
**NdisCmMakeCallComplete** 
**NdisCmModifyCallQoSComplete** 
**NdisCmNotifyCloseAddressFamily** 
**NdisCmOpenAddressFamilyComplete** 
**NdisCmRegisterAddressFamilyEx** 
**NdisCmRegisterSapComplete**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_CallManager_Function</strong>規則を指定します。</p>
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

[**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) 
[**NdisCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmaddpartycomplete) 
[**NdisCmCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmcloseaddressfamilycomplete) 
[**NdisCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete) 
[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 
[**NdisCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmderegistersapcomplete) 
[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected) 
[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall) 
[**NdisCmDispatchIncomingCallQoSChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange) 
[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall) 
[**NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingdropparty) 
[**NdisCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete) 
[**NdisCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmakecallcomplete) 
[**NdisCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmodifycallqoscomplete) 
[**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily) 
[**NdisCmOpenAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmopenaddressfamilycomplete) 
[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex) 
[**NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregistersapcomplete)








