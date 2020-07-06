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
ms.openlocfilehash: bb603369a09f83e337075ac8a0cfacbe43b1f593
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968415"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming rule (ndis)


**WlanConnectionRoaming**ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 接続とローミングシーケンスに正しく従っていることを確認します。

**ドライバーモデル: NDIS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00093005)


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
 

 





