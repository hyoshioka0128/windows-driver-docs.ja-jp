---
title: NdisOidDoubleComplete ルール (ndis)
description: NdisOidDoubleComplete ルールでは、NDIS ミニポート ドライバーが同じ OID の 2 回で NdisMOidRequestComplete ルーチンを呼び出す必要がないことを指定します。
ms.assetid: 876A3D3C-554F-4D71-AD1B-F568D0AD6C0D
ms.date: 05/21/2018
keywords:
- NdisOidDoubleComplete ルール (ndis)
topic_type:
- apiref
api_name:
- NdisOidDoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: affe756a47d4c3dd5d15ed569cbdf806d41f7a29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577910"
---
# <a name="ndisoiddoublecomplete-rule-ndis"></a>NdisOidDoubleComplete ルール (ndis)


**NdisOidDoubleComplete**ルールでは、NDIS ミニポート ドライバーを呼び出してはならないことを指定します、 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)同じ OID の 2 回ルーチン。

OID の追跡 (履歴\_オブジェクト)。 カーネル デバッガーでこのエラーをデバッグするには、次のように使用します。 **! ndiskd.oid**デバッガー拡張機能。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00091002) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。 このルールはでテストされても、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

.

<a name="applies-to"></a>対象
----------

[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





