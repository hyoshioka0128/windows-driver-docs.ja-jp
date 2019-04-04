---
title: Irql\_フィルター\_ドライバー\_関数ルール (ndis)
description: Irql\_フィルター\_ドライバー\_関数の規則は、適切な IRQL レベルでフィルター ドライバーの NDIS 関数を呼び出す必要がありますを指定します。
ms.assetid: 1dd45962-151b-472c-88a6-6042ecb7491c
ms.date: 05/21/2018
keywords:
- Irql_Filter_Driver_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Filter_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3b5217ae58c69ae4f1a7949fe95617aea7fe25b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548991"
---
# <a name="irqlfilterdriverfunction-rule-ndis"></a>Irql\_フィルター\_ドライバー\_関数ルール (ndis)


Irql\_フィルター\_ドライバー\_関数の規則は、適切な IRQL レベルでフィルター ドライバーの NDIS 関数を呼び出す必要がありますを指定します。

NDIS フィルター ドライバー機能を以下に示します。

**NdisFRegisterFilterDriver**
**NdisFDeregisterFilterDriver**
**NdisFSetAttributes** 
 **NdisFRestartFilter**
**NdisFRestartComplete**
**NdisFPauseComplete** 
 **NdisFSendNetBufferLists**
**NdisFReturnNetBufferLists**
**NdisFSendNetBufferListsComplete** 
 **NdisFCancelSendNetBufferLists**
**NdisFIndicateReceiveNetBufferLists**
**NdisFNetPnPEvent** 
 **NdisFDevicePnPEventNotify**
**NdisEnumerateFilterModules**

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>Irql_Filter_Driver_Function</strong>ルール。</p>
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

[**NdisEnumerateFilterModules**](https://msdn.microsoft.com/library/windows/hardware/ff561758)
[**NdisFCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561794) 
 [ **NdisFDeregisterFilterDriver**](https://msdn.microsoft.com/library/windows/hardware/ff561800)
[**NdisFDevicePnPEventNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff561804) 
 [ **NdisFIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561820)
[**NdisFNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561828) 
 [ **NdisFPauseComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561839)
[**NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608) 
 [ **NdisFRestartComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562610)
[**NdisFRestartFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff562611) 
 [ **NdisFReturnNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff562613)
[**NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616) 
 [ **NdisFSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562618)
[**NdisFSetAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff562619)








