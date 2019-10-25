---
title: 再構築された NET_BUFFER_LIST 構造
description: 再構築された NET_BUFFER_LIST 構造
ms.assetid: 0bfbfef3-c3ac-4add-b3b8-a4c3a96c8baa
keywords:
- NET_BUFFER_LIST
- 再構築構造の WDK ネットワーク
- 親/子 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- リレーションシップ (WDK NET_BUFFER_LIST)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df57023a8360c92dab68a8e99fa78783477cfdaa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844863"
---
# <a name="reassembled-net_buffer_list-structures"></a>再構築した NET\_BUFFER\_LIST 構造体





NDIS ドライバーでは、既存の NET\_BUFFER\_LIST 構造から、再構築した[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を作成できます。 再構築された構造体は、複数のソース[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の元のデータを参照します。 ドライバーは、この種類の構造を使用して、多数の小さいバッファーを効率的に1つの大きなバッファーに結合できます。

次の図は、親の NET\_BUFFER\_LIST 構造体と、再構成された子構造との関係を示しています。

![親の net\-buffer\-list 構造体と再構成された子構造との関係を示す図 ](images/netbufferlistreassembled.png)

上の図には、親の[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、その親から派生した子構造が含まれています。 親構造体には、1つの[**net\_バッファー\_リスト\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造、および mdls がアタッチされた3つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体があります。 親の構造体の親ポインターが、派生構造ではないことを示す**NULL**です。

子の NET\_BUFFER\_LIST 構造体には、MDLs がアタッチされた1つの NET\_バッファー構造があります。 子の NET\_BUFFER\_LIST 構造体には、親の構造体へのポインターがあります。 **NULL**の場合、NET\_BUFFER\_LIST\_コンテキスト構造体ポインターは、子が NET\_BUFFER\_LIST\_context 構造体を持たないことを示します。

NDIS ドライバーは、 [**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)関数を呼び出して、フラグメント化された[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を再アセンブルします。 NDIS は、再構築された NET\_BUFFER\_LIST 構造体を使用して、新しい[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体と mdls を割り当てます。 NDIS は、再構築された構造体に\_コンテキスト構造の NET\_BUFFER\_LIST を割り当てません。 再構築された NET\_BUFFER 構造体と MDLs は、親の構造と同じデータを記述します。 データはコピーされません。

再構築された NET\_BUFFER\_LIST 構造体を作成するために、 **NdisAllocateReassembledNetBufferList**は、各親 NET\_buffer 構造体の*StartOffset*パラメーターに指定されたバイト数をスキップします。 **NdisAllocateReassembledNetBufferList**は、各親 NET\_バッファー構造の残りのデータを、再構築された1つの NET\_バッファー構造の MDL チェーンに連結します。 **NdisAllocateReassembledNetBufferList** retreats (で使用されているデータ領域を増やします) は、再構築された NET\_バッファー構造体を*DataOffsetDelta*で指定した量だけ増やします。

NDIS ドライバーは、 [**NdisFreeReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreereassemblednetbufferlist)関数を呼び出して、再構築された[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、関連付けられている[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体と MDL チェーンを解放します。

## <a name="related-topics"></a>関連トピック


[派生 NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)

 

 






