---
title: 複製された NET_BUFFER_LIST 構造
description: 複製された NET_BUFFER_LIST 構造
ms.assetid: efcf7d03-401e-46da-9ca3-8423af1e385a
keywords:
- NET_BUFFER_LIST
- 複製された構造の WDK ネットワーク
- 重複した構造の WDK ネットワーク
- 親/子 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- 子/親 NET_BUFFER_LIST リレーションシップの WDK ネットワーク
- リレーションシップ (WDK NET_BUFFER_LIST)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c3d243366f31995270bd02386cb8abdb6cf72a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838203"
---
# <a name="cloned-net_buffer_list-structures"></a>複製された NET\_BUFFER\_LIST 構造体





NDIS ドライバーは、複製された[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を既存の NET\_BUFFER\_list 構造から作成します。 複製された構造体は元の構造体のデータを参照します。 ドライバーは、この種類の構造を使用して、同じデータを複数のパスに効率的に転送できます。

次の図は、親の NET\_BUFFER\_LIST 構造と、複製された子構造との関係を示しています。

![親の net\-buffer\-list 構造体と複製された子構造との関係を示す図](images/netbufferlistclone.png)

上の図には、親の[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体と、その親から派生した子構造が含まれています。 親構造体には、1つの[**net\_バッファー\_リスト\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造、および mdls がアタッチされた1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造があります。 親の構造体の親ポインターが、派生構造ではないことを示す**NULL**です。

子の NET\_BUFFER\_LIST 構造体には、MDLs がアタッチされた1つの NET\_バッファー構造があります。 子の NET\_BUFFER\_リストには、親構造へのポインターがあります。 **NULL**の場合、NET\_BUFFER\_LIST\_コンテキスト構造体ポインターは、子が NET\_BUFFER\_LIST\_context 構造体を持たないことを示します。

ドライバーは、 [**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist)関数を呼び出して、複製[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を作成します。 NDIS は、複製された NET\_BUFFER\_LIST 構造体を使用して、新しい[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体と mdls を割り当てます。 NDIS では、複製された構造体の[ **\_コンテキスト構造の NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)に割り当てられません。 新しい NET\_BUFFER 構造体と MDLs には、親構造と同じデータが記述されています。 データはコピーされません。

ドライバーは、 [**NdisFreeCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeclonenetbufferlist)関数を呼び出して **、net\_buffer\_LIST 構造体と、以前に割り当てられていたすべての関連する net\_buffer 構造体と MDL チェーンを解放します。NdisAllocateCloneNetBufferList**。

## <a name="related-topics"></a>関連トピック


[派生 NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)

 

 






