---
title: WlanAssociation ルール (ndis)
description: WlanAssociation ルールは、正しく、ミニポート ドライバーが依存しているネイティブの 802.11 ワイヤレス LAN (WLAN) の関連付けのシーケンスを確認します。
ms.assetid: 3F457C06-29F1-4730-92D5-5B98CD459FD1
ms.date: 05/21/2018
keywords:
- WlanAssociation ルール (ndis)
topic_type:
- apiref
api_name:
- WlanAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7bd8cc9f8622f63aeaa0dc9ca807f15655234436
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570888"
---
# <a name="wlanassociation-rule-ndis"></a>WlanAssociation ルール (ndis)


**WlanAssociation**ミニポート ドライバーが正しくネイティブ 802.11 ワイヤレス LAN (WLAN) の関連付けのシーケンスを次の規則を確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093004) |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を選択し、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn312128" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/dn312128)">NDIS/WIFI 検証</a>オプション。</p></td>
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

[接続の一般的な操作のガイドライン](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[OID\_DOT11\_リセット\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569409)
[NDIS\_状態\_DOT11\_アソシエーション\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567321)
 

 





