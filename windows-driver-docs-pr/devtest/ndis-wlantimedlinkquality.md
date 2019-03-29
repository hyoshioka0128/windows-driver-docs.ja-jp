---
title: WlanTimedLinkQuality ルール (ndis)
description: WlanTimedLinkQuality ルールの指定、NDIS\_状態\_DOT11\_リンク\_品質を示す値が成功した NDIS 後 15 秒以内に行われた\_状態\_DOT11\_アソシエーション\_完了します。
ms.assetid: B7055493-C09B-4565-A10F-32A34CCD5621
ms.date: 05/21/2018
keywords:
- WlanTimedLinkQuality ルール (ndis)
topic_type:
- apiref
api_name:
- WlanTimedLinkQuality
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc8b8591dcfaca727f64c0309e8308355f360090
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572226"
---
# <a name="wlantimedlinkquality-rule-ndis"></a>WlanTimedLinkQuality ルール (ndis)


**WlanTimedLinkQuality**規則の指定、NDIS\_状態\_DOT11\_リンク\_品質を示す値が成功した NDIS 後 15 秒以内に行われた\_状態\_DOT11\_アソシエーション\_完了します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0009400B) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/hh454208)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) 
 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)も参照してください
--------

[NDIS\_状態\_DOT11\_リンク\_品質](https://msdn.microsoft.com/library/windows/hardware/ff567344)
 

 





