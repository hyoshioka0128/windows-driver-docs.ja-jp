---
title: Irql \_ インターフェイス \_ 関数ルール (ndis)
description: Irql \_ interface \_ 関数ルールは、NDIS ネットワークインターフェイス関数を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: cea79975-4b14-4c7e-acfe-0bb10679e25b
ms.date: 05/21/2018
keywords:
- Irql_Interfaces_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_Interfaces_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55ddadc4542085791cef9ce3a7e021fb87188b82
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916465"
---
# <a name="irql_interfaces_function-rule-ndis"></a>Irql \_ インターフェイス \_ 関数ルール (ndis)


Irql \_ interface \_ 関数ルールは、NDIS ネットワークインターフェイス関数を正しい Irql レベルで呼び出す必要があることを指定します。

このルールは、次の NDIS ネットワークインターフェイス機能を検証します。

**NdisIfAddIfStackEntry** 
**NdisIfAllocateNetLuidIndex** 
**NdisIfDeleteIfStackEntry** 
**NdisIfDeregisterInterface** 
**NdisIfDeregisterProvider** 
**NdisIfFreeNetLuidIndex** 
**NdisIfGetInterfaceIndexFromNetLuid** 
**NdisIfGetNetLuidFromInterfaceIndex** 
**NdisIfQueryBindingIfIndex** 
**NdisIfRegisterInterface** 
**NdisIfRegisterProvider**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Interfaces_Function</strong>規則を指定します。</p>
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

[**NdisIfAddIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry) 
[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex) 
[**NdisIfDeleteIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifdeleteifstackentry) 
[**NdisIfDeregisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterinterface) 
[**NdisIfDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider) 
[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex) 
[**NdisIfGetInterfaceIndexFromNetLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid) 
[**NdisIfGetNetLuidFromInterfaceIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex) 
[**NdisIfQueryBindingIfIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifquerybindingifindex) 
[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface) 
[**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)








