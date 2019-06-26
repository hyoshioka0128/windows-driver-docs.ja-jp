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
ms.openlocfilehash: 425f26b5f2086978306a164a945a4b63170c523e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391824"
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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortStartIo</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepool)
[**ExAllocatePoolWithQuota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquota)
[**ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag) 
 [ **Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)
[**ExAllocatePoolWithTagPriority** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority)
 [ **IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)
[**IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp) 
 [**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiallocateinstanceids)
[**MmAllocateNonCachedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmallocatenoncachedmemory) 
 [ **MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)
[**ZwAllocateLocallyUniqueId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwallocatelocallyuniqueid) 
 [ **ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)
 

 





