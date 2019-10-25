---
title: WlanTimedScan rule (ndis)
description: WlanTimedScan ルールは、WLAN スキャン操作が15秒以内に完了したことを確認します。
ms.assetid: 6BFA0DAD-00A4-43EB-A226-40E1B0892E91
ms.date: 05/21/2018
keywords:
- WlanTimedScan rule (ndis)
topic_type:
- apiref
api_name:
- WlanTimedScan
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6e91f8405d7787941da1ce9b01c992f50d83b51
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839343"
---
# <a name="wlantimedscan-rule-ndis"></a>WlanTimedScan rule (ndis)


**WlanTimedScan**ルールは、WLAN スキャン操作が15秒以内に完了したことを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0009400c) |

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

[**Miniporthaltex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)
[**Miniporthaltex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)
[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)関連項目
--------

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
[OID\_DOT11\_接続\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-connect-request)
\_\_[dot11\_接続\_開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start)
 

 





