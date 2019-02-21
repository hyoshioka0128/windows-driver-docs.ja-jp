---
title: WlanTimedAssociation ルール (ndis)
description: WlanTimedAssociation ルールでは、NDIS ミニポート ドライバーが 10 秒後にワイヤレス LAN (WLAN) の関連付け操作が完了したことを指定します。
ms.assetid: 6454C7CF-EC89-44E9-B835-3C2FE0FFB595
ms.date: 05/21/2018
keywords:
- WlanTimedAssociation ルール (ndis)
topic_type:
- apiref
api_name:
- WlanTimedAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 028b289fe60f649ff04b9516eb9176f3dc6b3960
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548899"
---
# <a name="wlantimedassociation-rule-ndis"></a>WlanTimedAssociation ルール (ndis)


**WlanTimedAssociation**ルールでは、NDIS ミニポート ドライバーが 10 秒後にワイヤレス LAN (WLAN) の関連付け操作が完了したことを指定します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00094007) |

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

 

<a name="applies-to"></a>適用対象
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**MiniportOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff559416)
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)も参照してください
--------

[接続の一般的な操作のガイドライン](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[OID\_DOT11\_リセット\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569409)
[NDIS\_状態\_DOT11\_アソシエーション\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567321)
 

 





