---
title: ネットワーク ドライバーのパケット構造
description: ネットワーク ドライバーのパケット構造
ms.assetid: 01989a73-3f68-431a-ab77-b61f03265c22
keywords:
- パケットの WDK ネットワーク
- ネットワーク ドライバー WDK、パケット
- ネットワーク データ WDK
- データの WDK ネットワーク
- ネットワーク パケットの構造体 WDK
- ネットワーク データ バッファー WDK
- データ バッファーの WDK ネットワーク
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bb369eb0794899f878d7cbee10fb16b452960e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357609"
---
# <a name="packet-structures-in-network-drivers"></a>ネットワーク ドライバーのパケット構造





NDIS 6.0 とそれ以降のバージョンでは、以上のレイヤー ドライバーを割り当てる[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)と[ **NET\_バッファー リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)ネットワーク パケットの情報を保持する構造体し、ネットワーク上のデータを送信できるように、[次へ] の下の NDIS ドライバーを構造体を送信します。 下位レベルのドライバーは、NET を割り当てる\_バッファーと NET\_バッファー\_リストの構造体を受信したデータを保持し、最大の構造体を渡すには、上位層のドライバーが関心があります。 場合によっては、以上のレイヤー ドライバーでは、構造体に割り当てを指定されたバッファーに受信したデータをコピーする下位レイヤーのドライバーの要求で下位層のドライバーに渡します。 NDIS 割り当ておよびネットワークを構成するサブ構造体を操作するための機能を提供する\_バッファーと NET\_バッファー\_リストの構造体。

NDIS ドライバーでネットワーク データ バッファーの構造の詳細については、次を参照してください。 [NET\_バッファー アーキテクチャ](net-buffer-architecture.md)します。

 

 





