---
title: NdisAllocateGenericObject ルール (ndis)
description: NdisAllocateGenericObject ルールでは、NdisAllocateGenericObject と NdisFreeGenericObject が異なる順序でと呼ばれることを指定します。 最終的な目標では、MiniportHaltEx の終了時にすべてのジェネリック オブジェクトが解放されるかどうかを確認します。
ms.assetid: A247B43F-1958-4A57-AA60-37C995A96DF7
ms.date: 05/21/2018
keywords:
- NdisAllocateGenericObject ルール (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateGenericObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6549eef3709f64b0e87e1d5fb0c17b3aa0fc19f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536789"
---
# <a name="ndisallocategenericobject-rule-ndis"></a>NdisAllocateGenericObject ルール (ndis)


**NdisAllocateGenericObject**ルールを指定する[ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)と[ **NdisFreeGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561850)代替の順序で呼び出されます。 最終的な目標はすべてジェネリック オブジェクトが解放されるかどうかを確認するときに[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)が終了します。

ルールは、3 つの異なる状態を使用します。 NDIS ジェネリック オブジェクトを割り当てまたは解放時の状態の変更。 場合は、NDIS 汎用オブジェクトがまだ割り当てられているときに、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)終了すると、ルールは失敗します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisAllocateGenericObject</strong>ルール。</p>
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

[**NdisAllocateGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561603)
[**NdisFreeGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561850)
 

 





