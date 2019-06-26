---
title: WlanTimedLinkQuality ルール (ndis)
description: WlanTimedLinkQuality ルールの指定、NDIS\_状態\_DOT11\_リンク\_品質を示す値が成功した NDIS 後 15 秒以内に行われた\_状態\_DOT11\_アソシエーション\_完了します。
ms.assetid: B7055493-C09B-4565-A10F-32A34CCD5621
ms.date: 05/21/2018
keywords:
- WlanTimedLinkQuality ルール (ndis)
topic_type:
- apiref
api_name:
- WlanTimedLinkQuality
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 76716ea9c151d4bb37c6f2784756672dada3b1aa
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392128"
---
# <a name="wlantimedlinkquality-rule-ndis"></a>WlanTimedLinkQuality ルール (ndis)


**WlanTimedLinkQuality**規則の指定、NDIS\_状態\_DOT11\_リンク\_品質を示す値が成功した NDIS 後 15 秒以内に行われた\_状態\_DOT11\_アソシエーション\_完了します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x0009400B) |

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
[**MiniportOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex) 
 [ **NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)も参照してください
--------

[NDIS\_状態\_DOT11\_リンク\_品質](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-link-quality)
 

 





