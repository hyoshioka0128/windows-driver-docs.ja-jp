---
title: WlanDisassociation ルール (ndis)
description: WlanDisassociation ルールは、ミニポート ドライバー正しくネイティブ 802.11 ワイヤレス LAN (WLAN) 関連付けの解除のシーケンスに従うことを確認します。
ms.assetid: E9C115D5-8522-4275-B874-1DB673AE23F2
ms.date: 05/21/2018
keywords:
- WlanDisassociation ルール (ndis)
topic_type:
- apiref
api_name:
- WlanDisassociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b217e6369b8dd06717cbed97dc0e7126a9bb6652
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352927"
---
# <a name="wlandisassociation-rule-ndis"></a>WlanDisassociation ルール (ndis)


**WlanDisassociation**ルールは、ミニポート ドライバー正しくネイティブ 802.11 ワイヤレス LAN (WLAN) 関連付けの解除のシーケンスに従うことを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093006) |

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
[NDIS\_状態\_DOT11\_戻せません](https://msdn.microsoft.com/library/windows/hardware/ff567334)
[NDIS\_状態\_DOT11\_アソシエーション\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567321)
 

 





