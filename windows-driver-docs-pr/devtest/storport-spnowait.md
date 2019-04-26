---
title: SpNoWait ルール (storport)
description: このルールは、待機、またはデータの割り当ては StartIo 内で実行していないことを確認します。
ms.assetid: 4E1FABD1-AA6B-4EA1-BDD8-0C7A46AFF19B
ms.date: 05/21/2018
keywords:
- SpNoWait ルール (storport)
topic_type:
- apiref
api_name:
- SpNoWait
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0dd838cb02c1d7d7630de1afef452e6848fc8454
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345692"
---
# <a name="spnowait-rule-storport"></a>SpNoWait ルール (storport)


このルールは、待機、またはデータの割り当ては内で実行していないことを検証**StartIo**します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpNoWait</strong>ルール。</p>
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

[**StorPortStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff567508)
[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)
[**ExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544501) 
 [ **ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)
[**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513) 
 [ **Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)
 [ **ExWaitForRundownProtectionRelease**](https://msdn.microsoft.com/library/windows/hardware/jj569378)
[**IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)
 [ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoWMIAllocateInstanceIds** ](https://msdn.microsoft.com/library/windows/hardware/ff550429) 
[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)
[**KeWaitForMutexObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553344)
 [ **Kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479) 
 [ **MmAllocatePagesForMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554482) 
 [ **ZwAllocateLocallyUniqueId**](https://msdn.microsoft.com/library/windows/hardware/ff566415)
[**ZwAllocateVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566416) 
 [ **ZwWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff567120)
 

 





