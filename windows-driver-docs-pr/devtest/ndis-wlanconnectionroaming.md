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
ms.openlocfilehash: 0f86676100072366aae4fb61127b5307f49a78e6
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392147"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming ルール (ndis)


**WlanConnectionRoaming**ミニポート ドライバーは、誤って、ネイティブの 802.11 ワイヤレス LAN (WLAN) 接続とローミングの順序に従ったルールを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00093005) |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">NDIS/WIFI 検証</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>対象
----------

[**MiniportHaltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)
[**NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)も参照してください
--------

[接続の一般的な操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
[NDIS\_状態\_DOT11\_接続\_開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start)
[OID\_DOT11\_リセット\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)
[NDIS\_状態\_DOT11\_ローミング\_開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-roaming-start)
 

 





