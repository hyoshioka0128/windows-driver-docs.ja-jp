---
title: NdisXxx 関数の呼び出しの違い
description: NdisXxx 関数の呼び出しの違い
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx functions WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00d53ab9f66eee375bcd84a348785f3ae85936ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834895"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 関数の呼び出しの違い





呼び出しマネージャーは、MCM ドライバーとは異なる呼び出しマネージャー関数のセットを呼び出します。 呼び出しマネージャーは**NdisCm_Xxx_** functions を呼び出し、mcm ドライバーは**NdisMCm_Xxx_** 関数を呼び出します。

MCM ドライバーは、接続指向クライアントと呼び出しマネージャーの両方が呼び出す**NdisCo_Xxx_** 関数を呼び出しません。 代わりに、MCM ドライバーは、次のような同等の**NdisMCm_Xxx_** 関数を呼び出します。

-   [**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc) の代わりに [**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)

-   [**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) の代わりに [**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)

-   [**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest) の代わりに [**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

-   [**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete) の代わりに [**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)

MCM ドライバーは、 [**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)と同等の呼び出しを必要としません。これは、呼び出しマネージャーとミニポートドライバーの間の送信インターフェイスが mcm ドライバーの内部にあるため、NDIS に対して非透過的であるためです。

 

 





