---
title: NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED
description: ミニポート ドライバーでは、NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED を使用して、運用上の Wi-Fi Direct グループ所有者の Wi-fi 関連付け要求フレームが受信されたことを示します。
ms.assetid: c207ada5-39fd-4326-9b62-4844d3bb01af
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: f02be039bb15e3eb46de568a6b0a0b166fc9178f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382179"
---
# <a name="ndisstatuswdiindicationapassociationrequestreceived"></a>NDIS\_状態\_WDI\_INDICATION\_AP\_アソシエーション\_要求\_受信日時


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_AP\_アソシエーション\_要求\_Wi-fi 関連付け要求フレームがされていることを示す受信日時運用上の Wi-Fi Direct グループ所有者を受信しました。 ホストが発行することがあります、 [OID\_WDI\_タスク\_送信\_AP\_アソシエーション\_応答](oid-wdi-task-send-ap-association-response.md)この要求。

| オブジェクト |
|--------|
| ポート   |

 

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                                     | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                   |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_受信\_アソシエーション\_要求\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-incoming-association-request-info) |                                |          | 受信の関連付け要求情報。 |

 

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

 

 




