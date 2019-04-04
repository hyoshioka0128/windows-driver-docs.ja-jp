---
title: Irql\_接続\_関数ルール (ndis)
description: Irql\_接続\_関数の規則は、適切な IRQL レベル プロトコル ドライバーの NDIS 接続関数を呼び出す必要がありますを指定します。
ms.assetid: 9721cb8a-ac70-4f2b-8bbd-809dc06548dc
ms.date: 05/21/2018
keywords:
- Irql_Connection_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Connection_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb5f684e3adb130316daa105fed4fa403cd36ddd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557193"
---
# <a name="irqlconnectionfunction-rule-ndis"></a>Irql\_接続\_関数ルール (ndis)


**Irql\_接続\_関数**ルールでは、適切な IRQL レベル プロトコル ドライバーの NDIS 接続関数を呼び出す必要がありますを指定します。

このルールは、次の NDIS 関数を確認します。

**NdisCoAssignInstanceNam**
**NdisCoCreateVc**
**NdisCoDeleteVc**
**NdisCoGetTapiCallId**
 **NdisCoOidRequest**
**NdisCoOidRequestComplete**
**NdisCoSendNetBufferLists**

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Connection_Function</strong>ルール。</p>
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

[**NdisCoAssignInstanceName**](https://msdn.microsoft.com/library/windows/hardware/ff561692)
[**NdisCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561696)
[**NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698) 
 [ **NdisCoGetTapiCallId**](https://msdn.microsoft.com/library/windows/hardware/ff561700)
[**NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)
 [ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)
[**NdisCoSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561728)








