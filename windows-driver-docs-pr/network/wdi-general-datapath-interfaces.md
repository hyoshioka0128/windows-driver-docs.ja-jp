---
title: WDI 一般データパス インターフェイス
description: このセクションでは、一般的な WDI データパスインターフェイスについて説明します。
ms.assetid: 5B40171C-4E5F-4C35-A6E7-1EA5181C02E8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5253cf0535a14bbcf828cf851646f75e20abf97a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842929"
---
# <a name="wdi-general-datapath-interfaces"></a>WDI 一般データパス インターフェイス


## <a name="80211-frame-handling-and-frame-metadata"></a>802.11 フレームの処理とフレームのメタデータ


802.11 フレームは、WDI と TAL の間で、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) (NBL) チェーンの形式で渡されます。 各 NBL は、1つの MSDU を表します。 NBL 構造体は、マクロを使用して、データバッファーに対する操作と、オペレーティングシステムによって設定された Wi-fi TX メタデータを含むメタデータへのアクセスを提供します。 構造体は、コンテキストと**Miniportreserved**よって提供されるメンバーによって拡張できます。 **Miniportreserved 0\]** は、 [**WDI\_FRAME\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)型のバッファーを指しています。 このバッファーは、TX パスの WDI と、コールバック[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)を介して RX パスの TAL によって割り当てられます。 TAL は、Minipor\[Tre 1\] を使用して、追加のフレームメタデータを格納します。

## <a name="datapath-management-requests-and-indications"></a>データパス管理の要求と指示


データパス管理の要求と参照関数のリファレンスについては、「 [WDI データパス Management Functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

## <a name="related-topics"></a>関連トピック


[**NDIS\_WDI\_DATA\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_data_api)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[*NdisWdiAllocateWiFiFrameMetaData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_allocate_wdi_frame_metadata)

[**WDI\_フレーム\_のメタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_frame_metadata)

 

 






