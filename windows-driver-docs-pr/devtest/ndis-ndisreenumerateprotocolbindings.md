---
title: NdisReEnumerateProtocolBindings ルール (ndis)
description: プロトコル ドライバーでは、ProtocolBindAdapterEx または ProtocolUnbindAdapterEx 関数のコンテキスト内から NdisReEnumerateProtocolBindings を呼び出すことはできません。
ms.assetid: A6BB5B25-B8F4-4D90-B325-DFEED9C4AA6A
ms.date: 05/21/2018
keywords:
- NdisReEnumerateProtocolBindings ルール (ndis)
topic_type:
- apiref
api_name:
- NdisReEnumerateProtocolBindings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2b020ec0c65b64e3dd75e7e607d31c51889c48fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531553"
---
# <a name="ndisreenumerateprotocolbindings-rule-ndis"></a>NdisReEnumerateProtocolBindings ルール (ndis)


プロトコル ドライバーに呼び出すことはできません[ **NdisReEnumerateProtocolBindings** ](https://msdn.microsoft.com/library/windows/hardware/ff564516)からのコンテキスト内で、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)または[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。 また、プロトコルのドライバーを呼び出すことはできません**NdisReEnumerateProtocolBindings**からのコンテキスト内で、 [ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)関数の場合、 *ProtocolBindingContext*パラメーターの*ProtocolNetPnPEvent*が NULL でないです。 ただし、プロトコルのドライバーを呼び出すことができます**NdisReEnumerateProtocolBindings**からのコンテキスト内で*ProtocolNetPnPEvent*場合*ProtocolBindingContext*は NULL です。 NULL *ProtocolBindingContext*値では、イベントがすべてのバインドに適用されることを示します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisReEnumerateProtocolBindings</strong>ルール。</p>
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

[**NdisReEnumerateProtocolBindings**](https://msdn.microsoft.com/library/windows/hardware/ff564516)
 

 





