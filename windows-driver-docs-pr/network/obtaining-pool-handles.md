---
title: プール ハンドルの取得
description: プール ハンドルの取得
ms.assetid: 752b0d64-2ca3-4dc0-a6cd-642e96af1f8f
keywords:
- プールの WDK ネットワークを処理します。
- プロトコル ドライバー WDK ネットワー キング、ハンドルのプール
- NDIS プロトコル ドライバー WDK には、プールを処理します。
- ミニポート ドライバー WDK ネットワー キング、ハンドルのプール
- NDIS ミニポート ドライバー WDK、ハンドルをプールします。
- 中間ドライバー WDK ネットワーク、po
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a2b132d4f371e0461511950017cd60e16a32fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354508"
---
# <a name="obtaining-pool-handles"></a>プール ハンドルの取得





次の NDIS プール割り当て関数には、リソースの割り当てを識別するハンドルが必要です。

-   [**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferpool)

-   [**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)

NDIS 6.0 のドライバーは、次のようなハンドルを取得します。

<a href="" id="protocol-drivers"></a>プロトコル ドライバー  
プロトコルのドライバーの呼び出し、 [ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)ハンドルを取得する関数。

<a href="" id="miniport-drivers"></a>ミニポート ドライバー  
NDIS 呼び出し、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)ミニポート ドライバーにハンドルを渡す関数。

<a href="" id="intermediate-drivers"></a>中間ドライバー  
中級レベルのドライバーの呼び出し、 [ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)プールで使用される送信操作と NDIS のハンドルを取得する関数を呼び出す*MiniportInitializeEx*にプールで使用される受信操作のため、中間のドライバーにハンドルを渡します。

<a href="" id="filter-drivers"></a>フィルター ドライバー  
NDIS 呼び出し、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)フィルター ドライバーにハンドルを渡す関数。

<a href="" id="other-drivers"></a>その他のドライバー  
ドライバーを呼び出すことができる場合、ドライバーは、上記の方法のいずれかで、ハンドルを取得することはできません、 [ **NdisAllocateGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)ハンドルを取得する関数。

 

 





