---
title: WlanTimedAssociation rule (ndis)
description: WlanTimedAssociation 規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) の関連付け操作を完了することを指定します。
ms.assetid: 6454C7CF-EC89-44E9-B835-3C2FE0FFB595
ms.date: 05/21/2018
keywords:
- WlanTimedAssociation rule (ndis)
topic_type:
- apiref
api_name:
- WlanTimedAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 61276d48d9ebe1b2b586ffeaa1cecf708b7f5a34
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916922"
---
# <a name="wlantimedassociation-rule-ndis"></a>WlanTimedAssociation rule (ndis)


**WlanTimedAssociation**規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) の関連付け操作を完了することを指定します。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証の \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00094007) |

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
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関連項目
--------

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines) 
[OID \_Dot11 \_ リセット \_ 要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request) 
 [NDIS \_ ステータス \_ dot11 \_ 関連付け \_ 開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-start)
 

 





