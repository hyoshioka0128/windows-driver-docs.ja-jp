---
title: WlanTimedLinkQuality rule (ndis)
description: WlanTimedLinkQuality ルールでは、ndis \_ \_ ステータスの \_ \_ dot11 関連付けが正常に完了してから15秒後に、ndis ステータス dot11 リンクの品質を示し \_ \_ \_ \_ ます。
ms.assetid: B7055493-C09B-4565-A10F-32A34CCD5621
ms.date: 05/21/2018
keywords:
- WlanTimedLinkQuality rule (ndis)
topic_type:
- apiref
api_name:
- WlanTimedLinkQuality
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fe9413ba5c190d063f8537daacbaf05bcb378f8
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916448"
---
# <a name="wlantimedlinkquality-rule-ndis"></a>WlanTimedLinkQuality rule (ndis)


**WlanTimedLinkQuality**ルールでは、ndis \_ \_ ステータスの \_ \_ dot11 関連付けが正常に完了してから15秒後に、ndis ステータス dot11 リンクの品質を示し \_ \_ \_ \_ ます。

**ドライバーモデル: NDIS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0009400b) |

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
[**Miniportoidrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)関連項目
--------

[NDIS \_ ステータス \_ DOT11 \_ リンクの \_ 品質](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-link-quality)
 

 





