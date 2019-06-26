---
title: Irql\_MCM\_関数ルール (ndis)
description: Irql\_MCM\_関数の規則は、適切な IRQL レベルでのドライバーの NDIS MCM 関数を呼び出す必要がありますを指定します。
ms.assetid: 8cd71bf0-92ee-409d-90e3-6bb0c14ebda4
ms.date: 05/21/2018
keywords:
- Irql_MCM_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_MCM_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c681516e0c9f64d4579391741cdb6b3a9445c1a4
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392328"
---
# <a name="irqlmcmfunction-rule-ndis"></a>Irql\_MCM\_関数ルール (ndis)


**Irql\_MCM\_関数**ルールでは、適切な IRQL レベルでのドライバーの NDIS MCM 関数を呼び出す必要がありますを指定します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>Irql_MCM_Function</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)
[**NdisMCmAddPartyComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmaddpartycomplete) 
 [ **NdisMCmCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcloseaddressfamilycomplete)
[**NdisMCmCloseCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmclosecallcomplete) 
 [ **NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)
[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeactivatevc)
[**NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc) 
 [ **NdisMCmDeregisterSapComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmderegistersapcomplete) 
 [ **NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchcallconnected)
[**NdisMCmDispatchIncomingCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcall) 
 [ **NdisMCmDispatchIncomingCallQoSChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange)
[**NdisMCmDispatchIncomingCloseCall** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingclosecall) 
 [ **NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdispatchincomingdropparty)
[**NdisMCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdroppartycomplete) 
 [ **NdisMCmMakeCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmmakecallcomplete) 
 [ **NdisMCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmmodifycallqoscomplete)
[**NdisMCmNotifyCloseAddressFamily** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmnotifycloseaddressfamily) 
 [**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)
[**NdisMCmOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete) 
[ **NdisMCmOpenAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmopenaddressfamilycomplete)
[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex) 
 [ **NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregistersapcomplete)
 

 





