---
title: WDI 一般データパス インターフェイス
description: このセクションには、一般的な WDI データパス インターフェイスがについて説明します
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e182e1c5515d2aca6d17f6ba6aee7d51f83d4e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387220"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 一般データパス インターフェイス


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 フレームの処理とフレームのメタデータ


WDI との形式で話して間 802.11 フレームで渡される[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) (NBL) チェーン。 各 NBL では、1 つ MSDU を表します。 マクロ、を通じては、NBL 構造体は、データ バッファーとオペレーティング システムの設定、Wi-fi TX メタデータを含むメタデータへのアクセスでの操作を提供します。 構造体は、そのコンテキストを使用して拡張および**MiniportReserved**メンバー。 **MiniportReserved\[0\]** 型のバッファーを指す[ **WDI\_フレーム\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)します。 コールバックを使用して RX パスで話してと TX パスが、WDI によって、このバッファーが割り当てられている[ *NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)します。 話して MiniportReserved を使用して\[1\]を追加するフレームのメタデータを格納します。

## <a name="datapath-management-requests-and-indications"></a>データパス管理要求と表示


データパス管理要求とを示す値関数のリファレンスを参照してください。 [WDI データパス管理機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

## <a name="related-topics"></a>関連トピック


[**NDIS\_WDI\_データ\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_wdi_data_api)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)

[**WDI\_フレーム\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)

 

 






