---
title: WlanTimedScan ルール (ndis)
description: WlanTimedScan ルールは、15 秒以内に WLAN のスキャン操作が完了したことを確認します。
ms.assetid: 6BFA0DAD-00A4-43EB-A226-40E1B0892E91
ms.date: 05/21/2018
keywords:
- WlanTimedScan ルール (ndis)
topic_type:
- apiref
api_name:
- WlanTimedScan
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 206d055272a03deaa60c404b8c7fa829dcd6f26a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529404"
---
# <a name="wlantimedscan-rule-ndis"></a>WlanTimedScan ルール (ndis)


**WlanTimedScan**ルールは、15 秒以内に WLAN のスキャン操作が完了したことを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0009400C) |

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
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) 
 [ **NdisMOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563622)も参照してください
--------

[接続の一般的な操作のガイドライン](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[OID\_DOT11\_CONNECT\_要求](https://msdn.microsoft.com/library/windows/hardware/ff569122)
[NDIS\_状態\_DOT11\_接続\_開始](https://msdn.microsoft.com/library/windows/hardware/ff567328)
 

 





