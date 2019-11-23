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
ms.openlocfilehash: de64d0c05dd10f574d202ba13592acc12698b06a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839349"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming rule (ndis)


**WlanConnectionRoaming**ルールは、ミニポートドライバーがネイティブ802.11 ワイヤレス LAN (WLAN) 接続とローミングシーケンスに正しく従っていることを確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xc4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00093005) |

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

[**Miniporthaltex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関連項目
--------

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
[NDIS\_の状態\_dot11\_接続\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-connection-start)
[の\_の](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)\_\_の
の\_\_[の\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-roaming-start)の
 

 





