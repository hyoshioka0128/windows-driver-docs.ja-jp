---
title: Irql\_インターフェイス\_関数ルール (ndis)
description: Irql\_インターフェイス\_関数の規則は、適切な IRQL レベルで NDIS ネットワーク インターフェイスの関数を呼び出す必要がありますを指定します。
ms.assetid: cea79975-4b14-4c7e-acfe-0bb10679e25b
ms.date: 05/21/2018
keywords:
- Irql_Interfaces_Function ルール (ndis)
topic_type:
- apiref
api_name:
- Irql_Interfaces_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56ad71bcc66460604f3fe6fb8873f782cba1e2e1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392336"
---
# <a name="irqlinterfacesfunction-rule-ndis"></a>Irql\_インターフェイス\_関数ルール (ndis)


Irql\_インターフェイス\_関数の規則は、適切な IRQL レベルで NDIS ネットワーク インターフェイスの関数を呼び出す必要がありますを指定します。

このルールは、次の NDIS ネットワーク インターフェイスの機能を確認します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>Irql_Interfaces_Function</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisIfAddIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifaddifstackentry)
[**NdisIfAllocateNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifallocatenetluidindex) 
 [ **NdisIfDeleteIfStackEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifdeleteifstackentry)
[**NdisIfDeregisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifderegisterinterface) 
 [ **NdisIfDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifderegisterprovider)
[**NdisIfFreeNetLuidIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiffreenetluidindex) 
 [ **NdisIfGetInterfaceIndexFromNetLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid)
[**NdisIfGetNetLuidFromInterfaceIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex) 
 [**NdisIfQueryBindingIfIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifquerybindingifindex)
[**NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface) 
 [ **NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider)








