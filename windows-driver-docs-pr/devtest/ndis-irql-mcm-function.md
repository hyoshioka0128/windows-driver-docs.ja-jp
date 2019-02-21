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
ms.openlocfilehash: b32d8424fee67e567be122b6ebf84699eaa0d6ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537829"
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_MCM_Function</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisMCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562792)
[**NdisMCmAddPartyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562798) 
 [ **NdisMCmCloseAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562800)
[**NdisMCmCloseCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562803) 
 [ **NdisMCmCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562812)
[**NdisMCmDeactivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562818)
[**NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) 
 [ **NdisMCmDeregisterSapComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562821) 
 [ **NdisMCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff562826)
[**NdisMCmDispatchIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff562830) 
 [ **NdisMCmDispatchIncomingCallQoSChange**](https://msdn.microsoft.com/library/windows/hardware/ff563540)
[**NdisMCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff563541) 
 [ **NdisMCmDispatchIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff563542)
[**NdisMCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563543) 
 [ **NdisMCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563544) 
 [ **NdisMCmModifyCallQoSComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563545)
[**NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546) 
 [**NdisMCmOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563548)
[**NdisMCmOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563551) 
[ **NdisMCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563552)
[**NdisMCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff563554) 
 [ **NdisMCmRegisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563557)
 

 





