---
title: NdisReEnumerateProtocolBindings rule (ndis)
description: プロトコルドライバーは、ProtocolBindAdapterEx または ProtocolUnbindAdapterEx 関数のコンテキスト内から NdisReEnumerateProtocolBindings を呼び出すことはできません。
ms.assetid: A6BB5B25-B8F4-4D90-B325-DFEED9C4AA6A
ms.date: 05/21/2018
keywords:
- NdisReEnumerateProtocolBindings rule (ndis)
topic_type:
- apiref
api_name:
- NdisReEnumerateProtocolBindings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 21d6802a154291d46fd8c3fc6ad627ccd00d4a2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839361"
---
# <a name="ndisreenumerateprotocolbindings-rule-ndis"></a>NdisReEnumerateProtocolBindings rule (ndis)


プロトコルドライバーは、 [*protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)または[*protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数のコンテキスト内から[**NdisReEnumerateProtocolBindings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)を呼び出すことはできません。 また、 *ProtocolNetPnPEvent*の*PROTOCOLBINDINGCONTEXT*パラメーターが NULL でない場合、プロトコルドライバーは[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数のコンテキスト内から**NdisReEnumerateProtocolBindings**を呼び出すことができません。 ただし、 *ProtocolBindingContext*が NULL の場合、プロトコルドライバーは*ProtocolNetPnPEvent*のコンテキスト内から**NdisReEnumerateProtocolBindings**を呼び出すことができます。 NULL *ProtocolBindingContext*値は、イベントがすべてのバインドに適用されることを示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>NdisReEnumerateProtocolBindings</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisReEnumerateProtocolBindings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)
 

 





