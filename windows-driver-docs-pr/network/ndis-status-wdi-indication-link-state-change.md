---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: ミニポート ドライバーを次の状況のいずれかを示す NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE を使用します。
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2151af5c3ec4ff9df9713b111a6bb4896dcd0db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384217"
---
# <a name="ndisstatuswdiindicationlinkstatechange"></a>NDIS\_状態\_WDI\_INDICATION\_リンク\_状態\_変更


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_リンク\_状態\_を次の状況のいずれかを示すために変更します。

-   リンク速度を変更します。
-   しきい値を超えるによって変更されたリンクの品質。 接続品質のヒントが WDI に設定されている場合、しきい値が 1\_接続\_品質\_低\_待機時間 (で定義されている[ **WDI\_接続\_品質\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint))。 それ以外の場合、しきい値には 5 です。

| オブジェクト |
|--------|
| ポート   |

 

この通知からこの情報は、現在のリンクについてのメタデータを追跡する、ホストによって使用され、ユーザーにされる可能性があります。

ステーションと P2P クライアントの場合、ピアの MAC アドレスは、接続されたネットワークの BSSID に設定されます。 アジア太平洋/P2P の移動の場合は、ピアの MAC アドレスは、特定の接続されたデバイスの MAC アドレスに設定されます。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                           | 許可されている複数の TLV インスタンス | 省略可能 | 説明                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_リンク\_状態\_変更\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-link-state-change-parameters) |                                |          | リンクの状態は、パラメーターを変更します。 |

 

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

 

 




