---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: ミニポートドライバーは、NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE を使用して、次のいずれかの状況を示します。
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: a4a3416109e63b64fbc9c5fc65d9d35d4382deed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844428"
---
# <a name="ndis_status_wdi_indication_link_state_change"></a>NDIS\_STATUS\_WDI\_示さ\_リンク\_状態\_変更


ミニポートドライバーは、次のいずれかの状況を示すために、NDIS\_STATUS\_WDI\_\_リンク\_状態\_変更を使用します。

-   リンク速度が変更されました。
-   リンクの品質がしきい値を超えて変更されました。 接続品質ヒントが WDI に設定されている場合、しきい値は1になります。\_接続\_品質\_低\_待機時間 ( [**WDI\_接続\_品質\_ヒント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)で定義) です。 それ以外の場合、しきい値は5です。

| オブジェクト |
|--------|
| ポート   |

 

この表示の情報は、現在のリンクに関するメタデータを追跡するためにホストによって使用され、ユーザーに伝達される場合があります。

ステーションと P2P クライアントの場合、ピアの MAC アドレスは接続されたネットワークの BSSID に設定されます。 AP/P2P の場合、ピアの MAC アドレスは、特定の接続されたデバイスの MAC アドレスに設定されます。

## <a name="payload-data"></a>ペイロードデータ


| タスクバーの検索ボックスに                                                                                           | 複数の TLV インスタンスを使用できます | オプション | 説明                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_LINK\_の状態\_変更\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-link-state-change-parameters) |                                |          | リンクの状態変更パラメーター。 |

 

<a name="requirements"></a>要件
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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

 




