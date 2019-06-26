---
title: WlanAssociation ルール (ndis)
description: WlanAssociation ルールは、正しく、ミニポート ドライバーが依存しているネイティブの 802.11 ワイヤレス LAN (WLAN) の関連付けのシーケンスを確認します。
ms.assetid: 3F457C06-29F1-4730-92D5-5B98CD459FD1
ms.date: 05/21/2018
keywords:
- WlanAssociation ルール (ndis)
topic_type:
- apiref
api_name:
- WlanAssociation
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab7d1bdf65bf3d8a6c341d390f86ed50b8aec5d8
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392150"
---
# <a name="wlanassociation-rule-ndis"></a>WlanAssociation ルール (ndis)


**WlanAssociation**ミニポート ドライバーが正しくネイティブ 802.11 ワイヤレス LAN (WLAN) の関連付けのシーケンスを次の規則を確認します。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00093004) |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプション。</p></td>
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

[接続の一般的な操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
[OID\_DOT11\_リセット\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)
[NDIS\_状態\_DOT11\_アソシエーション\_開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-start)
 

 





