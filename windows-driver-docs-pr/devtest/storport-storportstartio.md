---
title: StorPortStartIo ルール (storport)
description: ミニポートの StartIo ルーチンで、待機、またはデータの割り当てを実行しない必要があります。
ms.assetid: 88CC6D8E-A493-4094-B30B-F6AE67A84B0F
ms.date: 05/21/2018
keywords:
- StorPortStartIo ルール (storport)
topic_type:
- apiref
api_name:
- StorPortStartIo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06d91e44a611c743c7fb29e55de8440797c6a6b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582692"
---
# <a name="storportstartio-rule-storport"></a>StorPortStartIo ルール (storport)


待機またはデータ割り当てする必要があります、ミニポートのでは実行しないで**StartIo**ルーチン。 呼び出す場合、ドライバーは、ルールが失敗した**StorPortStallExecution**または時間のかかる操作を含む別の関数。 **StartIo**が同期されると、これらの呼び出しはほとんどの場合で行う**BuildIo**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortStartIo</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)
[**ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)
[**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513) 
 [ **Exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)
 [ **IoAllocateController**](https://msdn.microsoft.com/library/windows/hardware/ff548224)
[**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257) 
 [**IoWMIAllocateInstanceIds**](https://msdn.microsoft.com/library/windows/hardware/ff550429)
[**MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479) 
 [ **MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)
[**ZwAllocateLocallyUniqueId** ](https://msdn.microsoft.com/library/windows/hardware/ff566415) 
 [ **ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)
 

 





