---
title: Irql\_ネットワーク\_関数ルール (ndis)
description: Irql\_ネットワーク\_関数の規則を指定する、NET\_バッファー関連の関数は、適切な IRQL レベルで呼び出す必要があります。
ms.assetid: e3b43ba1-3b58-4bc8-9d90-7be31c9e0a09
ms.date: 05/21/2018
keywords:
- Irql_NetBuffer_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_NetBuffer_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97bdde0cf34405cac21736725d3355d24e896a9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531193"
---
# <a name="irqlnetbufferfunction-rule-ndis"></a>Irql\_ネットワーク\_関数ルール (ndis)


Irql\_ネットワーク\_関数の規則を指定する、NET\_バッファー関連の関数は、適切な IRQL レベルで呼び出す必要があります。

このルールは、次の NDIS 関数を確認します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_NetBuffer_Function</strong>ルール。</p>
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

[**NdisAdvanceNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560703)
[**NdisAdvanceNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff560704)
[**NdisAllocateCloneNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560705)
[**NdisAllocateFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560707)
[**NdisAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff561605)
[**NdisAllocateNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561607)
[**NdisAllocateNetBufferAndNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561608)
[**NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609)
[**NdisAllocateNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff561610)
[**NdisAllocateNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff561611)
[**NdisAllocateNetBufferMdlAndData**](https://msdn.microsoft.com/library/windows/hardware/ff561612)
[**NdisAllocateNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff561613)
[**NdisAllocateReassembledNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561614)
[**NdisCopyFromNetBufferToNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff561718)
[**NdisCopyReceiveNetBufferListInfo**](https://msdn.microsoft.com/library/windows/hardware/ff561722)
[**NdisCopySendNetBufferListInfo**](https://msdn.microsoft.com/library/windows/hardware/ff561724)
[**NdisFreeCloneNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561841)
[**NdisFreeFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561847)
[**NdisFreeMdl**](https://msdn.microsoft.com/library/windows/hardware/ff562575)
[**NdisFreeNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562582)
[**NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)
[**NdisFreeNetBufferListContext**](https://msdn.microsoft.com/library/windows/hardware/ff562587)
[**NdisFreeNetBufferListPool**](https://msdn.microsoft.com/library/windows/hardware/ff562590)
[**NdisFreeNetBufferPool**](https://msdn.microsoft.com/library/windows/hardware/ff562592)
[**NdisFreeReassembledNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562594)
[**NdisGetDataBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562631)
[**NdisGetMdlPhysicalArraySize**](https://msdn.microsoft.com/library/windows/hardware/ff562639)
[**NdisGetPoolFromNetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff562657)
[**NdisGetPoolFromNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562659)
[**NdisQueryMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563757)
[**NdisQueryMdlOffset**](https://msdn.microsoft.com/library/windows/hardware/ff563761)
[**NdisQueryNetBufferPhysicalCount**](https://msdn.microsoft.com/library/windows/hardware/ff563766)
[**NdisRetreatNetBufferDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564527)
[**NdisRetreatNetBufferListDataStart**](https://msdn.microsoft.com/library/windows/hardware/ff564529)








