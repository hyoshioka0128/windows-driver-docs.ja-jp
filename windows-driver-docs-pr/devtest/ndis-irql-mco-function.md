---
title: Irql\_MCO\_関数ルール (ndis)
description: Irql\_MCO\_関数の規則は、適切な IRQL レベルでのミニポート ドライバーの NDIS MCO Ddi を呼び出す必要があることを指定します。
ms.assetid: 4a6643a2-d831-4b60-a9d6-decf494a2ffc
ms.date: 05/21/2018
keywords:
- Irql_MCO_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_MCO_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d72092554e646d7785bf658317cd422bd28c6764
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572622"
---
# <a name="irqlmcofunction-rule-ndis"></a>Irql\_MCO\_関数ルール (ndis)


**Irql\_MCO\_関数**ルールでは、適切な IRQL レベルでのミニポート ドライバーの NDIS MCO Ddi を呼び出す必要があることを指定します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_MCO_Function</strong>ルール。</p>
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

[**NdisMCoActivateVcComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563558)
[**NdisMCoDeactivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563559) 
 [ **NdisMCoIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563561)
[**NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562) 
 [ **NdisMCompleteDmaTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff563564)
[**NdisMCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563568) 
 [ **NdisMCoSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563570)
 

 





