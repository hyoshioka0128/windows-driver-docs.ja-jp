---
title: ネットワーク ドライバーのパケット構造
description: ネットワーク ドライバーのパケット構造
ms.assetid: 01989a73-3f68-431a-ab77-b61f03265c22
keywords:
- パケット WDK ネットワーク
- ネットワークドライバー WDK、パケット
- ネットワークデータ WDK
- データ WDK ネットワーク
- ネットワークパケット構造 (WDK)
- ネットワークデータバッファー WDK
- データバッファー WDK ネットワーク
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bc20f1fb93f2991fe2ef7f39af883f98e18939a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843705"
---
# <a name="packet-structures-in-network-drivers"></a>ネットワーク ドライバーのパケット構造





NDIS 6.0 以降のバージョンでは、より上位のレイヤードライバーがネットワークパケット情報を保持するために、 [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)と[**NET\_buffer LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を割り当て、次に低い NDIS ドライバーにデータを送信できるように構造を送信します。ネットワーク。 下位レベルのドライバーは、受信したデータを保持するために NET\_BUFFER と NET\_BUFFER\_リスト構造体を割り当て、それに関連する上位層のドライバーに構造体を渡します。 場合によっては、より上位のレイヤードライバーが構造体を割り当て、下位層のドライバーに渡します。下位層ドライバーは、指定されたバッファーに受信したデータをコピーするように要求します。 NDIS には、NET\_BUFFER と NET\_BUFFER\_リスト構造を構成するサブ構造体の割り当てと操作を行うための関数が用意されています。

NDIS ドライバーのネットワークデータバッファーの構造の詳細については、「 [NET\_のバッファーアーキテクチャ](net-buffer-architecture.md)」を参照してください。

 

 





