---
title: Irql \_ netbuffer \_ 関数規則 (ndis)
description: Irql \_ netbuffer 関数ルールでは、 \_ \_ 正しい Irql レベルで、NET バッファー関連の関数を呼び出す必要があることを指定します。
ms.assetid: e3b43ba1-3b58-4bc8-9d90-7be31c9e0a09
ms.date: 05/21/2018
keywords:
- Irql_NetBuffer_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_NetBuffer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 206f3a66d4f933099e5e20a70d9f08da055cab25
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916522"
---
# <a name="irql_netbuffer_function-rule-ndis"></a>Irql \_ netbuffer \_ 関数規則 (ndis)


Irql \_ netbuffer 関数ルールでは、 \_ \_ 正しい Irql レベルで、NET バッファー関連の関数を呼び出す必要があることを指定します。

このルールは、次の NDIS 関数を検証します。

**NdisAdvanceNetBufferDataStart** 
**disAdvanceNetBufferListDataStart** 
**NdisAllocateCloneNetBufferList** 
**NdisAllocateFragmentNetBufferList** 
**NdisAllocateMdl** 
**NdisAllocateNetBuffer** 
**NdisAllocateNetBufferAndNetBufferList** 
**NdisAllocateNetBufferList** 
**NdisAllocateNetBufferListContext** 
**NdisAllocateNetBufferListPool** 
**NdisAllocateNetBufferMdlAndData** 
**NdisAllocateNetBufferPool** 
**NdisAllocateReassembledNetBufferList** 
**NdisCopyFromNetBufferToNetBuffer** 
**NdisCopyReceiveNetBufferListInfo** 
**NdisCopySendNetBufferListInfo** 
**NdisFreeCloneNetBufferList** 
**NdisFreeFragmentNetBufferList** 
**NdisFreeMdl** 
**NdisFreeNetBuffer** 
**NdisFreeNetBufferList** 
**NdisFreeNetBufferListContext** 
**NdisFreeNetBufferListPool** 
**NdisFreeNetBufferPool** 
**NdisFreeReassembledNetBufferList** 
**NdisGetDataBuffer** 
**NdisGetMdlPhysicalArraySize** 
**NdisGetPoolFromNetBuffer** 
**NdisGetPoolFromNetBufferList** 
**NdisQueryMdl** 
**NdisQueryMdlOffset** 
**NdisQueryNetBufferPhysicalCount** 
**NdisRetreatNetBufferDataStart** 
**NdisRetreatNetBufferListDataStart**

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_NetBuffer_Function</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart) 
[**NdisAdvanceNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferlistdatastart) 
[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist) 
[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist) 
[**NdisAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatemdl) 
[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer) 
[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist) 
[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist) 
[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistcontext) 
[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool) 
[**NdisAllocateNetBufferMdlAndData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffermdlanddata) 
[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool) 
[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist) 
[**NdisCopyFromNetBufferToNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopyfromnetbuffertonetbuffer) 
[**NdisCopyReceiveNetBufferListInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopyreceivenetbufferlistinfo) 
[**NdisCopySendNetBufferListInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscopysendnetbufferlistinfo) 
[**NdisFreeCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeclonenetbufferlist) 
[**NdisFreeFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreefragmentnetbufferlist) 
[**NdisFreeMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreemdl) 
[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer) 
[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist) 
[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistcontext) 
[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool) 
[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool) 
[**NdisFreeReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreereassemblednetbufferlist) 
[**NdisGetDataBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetdatabuffer) 
[**NdisGetMdlPhysicalArraySize**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisgetmdlphysicalarraysize) 
[**NdisGetPoolFromNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetpoolfromnetbuffer) 
[**NdisGetPoolFromNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetpoolfromnetbufferlist) 
[**NdisQueryMdl**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisquerymdl) 
[**NdisQueryMdlOffset**](https://docs.microsoft.com/windows-hardware/drivers/network/ndisquerymdloffset) 
[**NdisQueryNetBufferPhysicalCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerynetbufferphysicalcount) 
[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart) 
[**NdisRetreatNetBufferListDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferlistdatastart)








