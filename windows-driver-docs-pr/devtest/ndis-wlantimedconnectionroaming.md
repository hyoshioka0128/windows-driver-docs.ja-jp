---
title: WlanTimedConnectionRoaming rule (ndis)
description: WlanTimedConnectionRoaming 規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) 接続/ローミング操作を完了することを指定します。
ms.assetid: 0961C34B-FAD8-49ED-A0FD-5D790E973C4D
ms.date: 05/21/2018
keywords:
- WlanTimedConnectionRoaming rule (ndis)
topic_type:
- apiref
api_name:
- WlanTimedConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e66b2a278e1fd426e996765497c876fdd864ebe5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916921"
---
# <a name="wlantimedconnectionroaming-rule-ndis"></a>WlanTimedConnectionRoaming rule (ndis)


**WlanTimedConnectionRoaming**規則は、NDIS ミニポートドライバーが10秒以内にワイヤレス LAN (WLAN) 接続/ローミング操作を完了することを指定します。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00094008) |

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
 

 





