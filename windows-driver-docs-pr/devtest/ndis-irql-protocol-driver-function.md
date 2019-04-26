---
title: Irql\_プロトコル\_ドライバー\_関数ルール (ndis)
description: Irql\_プロトコル\_ドライバー\_関数の規則は、適切な IRQL レベルにいる CoNDIS クライアントの NDIS 関数を呼び出す必要がありますを指定します。
ms.assetid: 9461c3d9-cb31-4ffd-b057-fd9978808c2f
ms.date: 05/21/2018
keywords:
- Irql_Protocol_Driver_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Protocol_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a3082c21af570a061f7069cf67941f837955e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347651"
---
# <a name="irqlprotocoldriverfunction-rule-ndis"></a>Irql\_プロトコル\_ドライバー\_関数ルール (ndis)


Irql\_プロトコル\_ドライバー\_関数の規則は、適切な IRQL レベルにいる CoNDIS クライアントの NDIS 関数を呼び出す必要がありますを指定します。

このルールは、次の NDIS 関数を確認します。

**NdisClAddParty**
**NdisClCloseAddressFamily**
**NdisClCloseCall**
**NdisClDeregisterSap** 
 **NdisClDropParty**
**NdisClGetProtocolVcContextFromTapiCallId**
**NdisClIncomingCallComplete** 
 **NdisClMakeCall**
**NdisClModifyCallQoS**
**NdisClNotifyCloseAddressFamilyComplete** 
 **NdisClOpenAddressFamilyEx**
**NdisCloseAdapterEx**
**NdisClRegisterSap** 
 **NdisCompleteBindAdapterEx**
**NdisCompleteNetPnPEvent**
**NdisCompleteUnbindAdapterEx**
 **NdisDeregisterProtocolDriver**
**NdisMNetPnPEvent**
**NdisOpenAdapterEx** 
 **NdisRegisterProtocolDriver**
**NdisUnbindAdapter**

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Protocol_Driver_Function</strong>ルール。</p>
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

[**NdisClAddParty**](https://msdn.microsoft.com/library/windows/hardware/ff561625)
[**NdisClCloseAddressFamily**](https://msdn.microsoft.com/library/windows/hardware/ff561626)
[**NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627) 
 [ **NdisClDeregisterSap**](https://msdn.microsoft.com/library/windows/hardware/ff561628)
[**NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)
 [ **NdisClGetProtocolVcContextFromTapiCallId**](https://msdn.microsoft.com/library/windows/hardware/ff561631)
[**NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632)
 [ **NdisClMakeCall**](https://msdn.microsoft.com/library/windows/hardware/ff561635)
[**NdisClModifyCallQoS** ](https://msdn.microsoft.com/library/windows/hardware/ff561636) 
 [**NdisClNotifyCloseAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561638)
[**NdisClOpenAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561639) 
[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)
[**NdisClRegisterSap** ](https://msdn.microsoft.com/library/windows/hardware/ff561648) 
[ **NdisCompleteBindAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561702)
[**NdisCompleteNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561705) 
 [ **NdisCompleteUnbindAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561708)
[**NdisDeregisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff561743) 
 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616) 
 [ **NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)
[**NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520) 
 [**NdisUnbindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff564630)








