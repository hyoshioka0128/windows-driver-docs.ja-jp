---
title: NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL を使用して、運用チャネルで動作している Wi-Fi Direct、特定のポートを示します。
ms.assetid: 170e5df7-3128-4942-869d-45206022dfaa
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 08ec77366e9ca507cede911b500594b8e9a628dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382657"
---
# <a name="ndisstatuswdiindicationp2pgroupoperatingchannel"></a>NDIS\_状態\_WDI\_INDICATION\_P2P\_グループ\_オペレーティング\_チャネル


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_INDICATION\_P2P\_グループ\_オペレーティング\_を示す Wi-Fi Direct ポートを特定のチャネル動作しているチャネルは、動作しています。

Wi-Fi Direct クライアント ポートには、これは (接続完了) の前に接続中に示す必要があります。

この、Wi-Fi Direct の移動のポートの中に表示する必要があります[OID\_WDI\_タスク\_開始\_AP](oid-wdi-task-start-ap.md) (完了する前に、OID)。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                         | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                        |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_チャネル\_数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number)                    |                                |          | 指定された Wi-Fi Direct ポートが動作している運用チャネル。 |
| [**WDI\_TLV\_P2P\_チャネル\_を示す\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-indicate-reason) |                                |          | 示す値を送信する理由です。                             |

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




