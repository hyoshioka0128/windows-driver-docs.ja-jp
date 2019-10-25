---
title: WlanTimedConnectRequest rule (ndis)
description: WlanTimedConnectRequest ルールでは、OID\_DOT11\_CONNECT\_要求の後に、\_DOT11\_接続\_\_から10秒以内に開始されることを確認します。
ms.assetid: F40D92B1-CA48-4060-B9E2-A965900EAF7B
ms.date: 05/21/2018
keywords:
- WlanTimedConnectRequest rule (ndis)
topic_type:
- apiref
api_name:
- WlanTimedConnectRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d3841717f03d90c80744fe9f78396ff8613fadd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839346"
---
# <a name="wlantimedconnectrequest-rule-ndis"></a>WlanTimedConnectRequest rule (ndis)


**WlanTimedConnectRequest**ルールでは、OID\_DOT11\_CONNECT\_要求の後に、\_DOT11\_接続\_\_から10秒以内に開始されることを確認します。

さらに、NDIS の\_状態\_DOT11\_接続の\_開始は、OID\_DOT11\_接続\_要求が、NDIS\_STATUS\_SUCCESS で完了した場合にのみ示されます。 このルールは、拡張ステーションのポート (ポート 0) にのみ適用されます。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00094009) |

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
 

 





