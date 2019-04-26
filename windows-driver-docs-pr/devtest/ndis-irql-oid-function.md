---
title: Irql\_OID\_関数ルール (ndis)
description: Irql\_OID\_関数の規則は、適切な IRQL レベルで NDIS OID 要求 Ddi を呼び出す必要があることを指定します。
ms.assetid: 450afd4e-ba01-45e8-a866-6cd9b3190bb7
ms.date: 05/21/2018
keywords:
- Irql_OID_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_OID_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe3a632e2cd7df959d0cfdf85ef2a69149f36c52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347643"
---
# <a name="irqloidfunction-rule-ndis"></a>Irql\_OID\_関数ルール (ndis)


**Irql\_OID\_関数**ルールでは、適切な IRQL レベルで NDIS OID 要求 Ddi を呼び出す必要があることを指定します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_OID_Function</strong>ルール。</p>
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

[**NdisAllocateCloneOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff560706)
[**NdisCancelOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561622)
[**NdisFCancelOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561792) 
 [ **NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)
[**NdisFOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561833) 
 [ **NdisFreeCloneOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561845)
[**NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 [ **NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)
 

 





