---
title: Irql\_CallManager\_関数ルール (ndis)
description: Irql\_CallManager\_関数の規則は、適切な IRQL レベルで NDIS CallManager の NDIS 関数を呼び出す必要がありますを指定します。
ms.assetid: 3e026fb0-8c5f-40cc-affb-3b35f17f40f7
ms.date: 05/21/2018
keywords:
- Irql_CallManager_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_CallManager_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f453fd4021e215dad8208600ac4c25b062388bc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559567"
---
# <a name="irqlcallmanagerfunction-rule-ndis"></a>Irql\_CallManager\_関数ルール (ndis)


**Irql\_CallManager\_関数**ルールでは、適切な IRQL レベルで NDIS CallManager の NDIS 関数を呼び出す必要がありますを指定します。

このルールは、次の NDIS 関数を調べます。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_CallManager_Function</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561649)
[**NdisCmAddPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561651)
[**NdisCmCloseAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561654) 
 [ **NdisCmCloseCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561655)
[**NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657) 
 [ **NdisCmDeregisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561659)
[**NdisCmDispatchCallConnected** ](https://msdn.microsoft.com/library/windows/hardware/ff561661) 
 [ **NdisCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff561664)
[**NdisCmDispatchIncomingCallQoSChange**](https://msdn.microsoft.com/library/windows/hardware/ff561668) 
 [ **NdisCmDispatchIncomingCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561670)
[**NdisCmDispatchIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff561672) 
 [ **NdisCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561674)
[**NdisCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561677) 
 [ **NdisCmModifyCallQoSComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561679) 
 [ **NdisCmNotifyCloseAddressFamily**](https://msdn.microsoft.com/library/windows/hardware/ff561680)
[**NdisCmOpenAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561682) 
[ **NdisCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561685)
[**NdisCmRegisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561689)








