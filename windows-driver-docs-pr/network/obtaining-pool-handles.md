---
title: プール ハンドルの取得
description: プール ハンドルの取得
ms.assetid: 752b0d64-2ca3-4dc0-a6cd-642e96af1f8f
keywords:
- プールは WDK ネットワークを処理します
- プロトコルドライバー WDK ネットワーク、プールハンドル
- NDIS プロトコルドライバー WDK、プールハンドル
- ミニポートドライバー WDK ネットワーク、プールハンドル
- NDIS ミニポートドライバー WDK、プールハンドル
- 中間ドライバー WDK ネットワーク、po
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3afff6a3b6b5f7616f47ca54e080ae917ad8d1ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837744"
---
# <a name="obtaining-pool-handles"></a>プール ハンドルの取得





次の NDIS プール割り当て関数では、リソースを割り当てるハンドルが必要です。

-   [**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

-   [**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

NDIS 6.0 ドライバーは、次のようにハンドルを取得します。

<a href="" id="protocol-drivers"></a>プロトコルドライバー  
プロトコルドライバーは、 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出してハンドルを取得します。

<a href="" id="miniport-drivers"></a>ミニポートドライバー  
NDIS は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出して、ハンドルをミニポートドライバーに渡します。

<a href="" id="intermediate-drivers"></a>中間ドライバー  
中間ドライバーは、 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出して、送信操作で使用されるプールと、受信操作で使用されるプールの中間ドライバーにハンドルを渡す*MiniportInitializeEx*のハンドルを取得します。

<a href="" id="filter-drivers"></a>ドライバーのフィルター  
NDIS は、フィルタードライバーにハンドルを渡す[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出します。

<a href="" id="other-drivers"></a>その他のドライバー  
ドライバーが、上記のいずれかの方法でハンドルを取得できない場合、ドライバーは[**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)関数を呼び出してハンドルを取得できます。

 

 





