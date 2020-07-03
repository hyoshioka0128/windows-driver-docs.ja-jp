---
title: WlanDisassociation rule (ndis)
description: WlanDisassociation ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 関連付けシーケンスに正しく従っていることを確認します。
ms.assetid: E9C115D5-8522-4275-B874-1DB673AE23F2
ms.date: 05/21/2018
keywords:
- WlanDisassociation rule (ndis)
topic_type:
- apiref
api_name:
- WlanDisassociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa2323c7e756887fbfb8a9d3d4cf55428049e8e7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916930"
---
# <a name="wlandisassociation-rule-ndis"></a>WlanDisassociation rule (ndis)


**WlanDisassociation**ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 関連付けシーケンスに正しく従っていることを確認します。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00093006) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**ミニ Porthaltex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 
[**Miniportoidrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)関連項目
--------

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines) 
[OID \_Dot11 \_ リセット \_ 要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request) 
 [NDIS \_ ステータス \_ dot11 \_ 関連付け](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-disassociation) 
 [NDIS \_ ステータス \_ dot11 \_ アソシエーション \_ 開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-start)
 

 





