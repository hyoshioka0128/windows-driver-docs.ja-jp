---
title: WlanConnectionRoaming ルール (ndis)
description: ミニポート ドライバーは、誤って、ネイティブの 802.11 ワイヤレス LAN (WLAN) 接続とローミングの順序に従った WlanConnectionRoaming ルールを確認します。
ms.assetid: 7DB1881B-4DD8-4E06-AAF2-C6EAD0EEC5FC
ms.date: 05/21/2018
keywords:
- WlanConnectionRoaming ルール (ndis)
topic_type:
- apiref
api_name:
- WlanConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fcf284c92c6f288d3118e341a6edc727f72bba5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531153"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming ルール (ndis)


**WlanConnectionRoaming**ミニポート ドライバーは、誤って、ネイティブの 802.11 ワイヤレス LAN (WLAN) 接続とローミングの順序に従ったルールを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093005) |

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

 

<a name="applies-to"></a>適用対象
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)も参照してください
--------

[接続の一般的な操作のガイドライン](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[NDIS\_状態\_DOT11\_接続\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567328)
[OID\_DOT11\_リセット\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569409)
[NDIS\_状態\_DOT11\_ローミング\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567360)
 

 





