---
title: Irql\_同期\_関数ルール (ndis)
description: Irql\_同期\_関数ルール NDIS 割り込みと同期 Ddi する必要があります呼び出すように指定適切な IRQL レベル。
ms.assetid: 5d0e862a-89e6-493d-a102-83430c5140e4
ms.date: 05/21/2018
keywords:
- Irql_Synch_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Synch_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f34463959973602e0f6433dc3b820bc53bf72f8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347629"
---
# <a name="irqlsynchfunction-rule-ndis"></a>Irql\_同期\_関数ルール (ndis)


**Irql\_同期\_関数**ルール NDIS 割り込みと同期 Ddi する必要があります呼び出すように指定適切な IRQL レベル。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Synch_Function</strong>ルール。</p>
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

[**NDIS\_リリース\_ミュー テックス**](https://msdn.microsoft.com/library/windows/hardware/ff567247)
[**NDIS\_待機\_の\_ミュー テックス**](https://msdn.microsoft.com/library/windows/hardware/ff567897)
 [ **NdisAcquireReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff560696)
[**NdisAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff560699) 
 [ **NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)
[**NdisDprReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561753) 
 [**NdisReleaseReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff564521)
[**NdisReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff564524) 
 [ **NdisResetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff564526)
[**NdisSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff564539)
 

 





