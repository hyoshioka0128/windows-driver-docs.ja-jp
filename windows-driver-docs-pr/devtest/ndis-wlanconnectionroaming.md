---
title: WlanConnectionRoaming rule (ndis)
description: WlanConnectionRoaming ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 接続とローミングシーケンスに正しく従っていることを確認します。
ms.assetid: 7DB1881B-4DD8-4E06-AAF2-C6EAD0EEC5FC
ms.date: 05/21/2018
keywords:
- WlanConnectionRoaming rule (ndis)
topic_type:
- apiref
api_name:
- WlanConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5857ac22dba7d588804c54f193916586b2bd403
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916923"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming rule (ndis)


**WlanConnectionRoaming**ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 接続とローミングシーケンスに正しく従っていることを確認します。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00093005) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">NDIS/WIFI 検証</a>オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**ミニ Porthaltex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関連項目
--------

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines) 
[NDIS \_ステータス \_ dot11 \_ 接続 \_ 開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start) 
 [OID \_ DOT11 \_ リセット \_ 要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request) 
 [NDIS \_ ステータス \_ DOT11 \_ ローミング \_ 開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-roaming-start)
 

 





