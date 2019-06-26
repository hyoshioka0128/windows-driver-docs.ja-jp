---
title: WlanTimedConnectionRoaming ルール (ndis)
description: WlanTimedConnectionRoaming ルールでは、NDIS ミニポート ドライバーが 10 秒以内に、ワイヤレス LAN (WLAN) 接続/移動操作を完了するを指定します。
ms.assetid: 0961C34B-FAD8-49ED-A0FD-5D790E973C4D
ms.date: 05/21/2018
keywords:
- WlanTimedConnectionRoaming ルール (ndis)
topic_type:
- apiref
api_name:
- WlanTimedConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d23c2cf160707e277cfe9839ef752190386de089
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392140"
---
# <a name="wlantimedconnectionroaming-rule-ndis"></a>WlanTimedConnectionRoaming ルール (ndis)


**WlanTimedConnectionRoaming**ルールでは、NDIS ミニポート ドライバーが 10 秒以内に、ワイヤレス LAN (WLAN) 接続/移動操作を完了するを指定します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00094008) |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**MiniportHaltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)
[**MiniportOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)も参照してください
--------

[接続の一般的な操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
 

 





