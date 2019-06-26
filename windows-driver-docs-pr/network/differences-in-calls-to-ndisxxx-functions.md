---
title: NdisXxx 関数の呼び出しの違い
description: NdisXxx 関数の呼び出しの違い
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a4a3f7138c93e35f97a337b46d8dea309af57f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381379"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 関数の呼び出しの違い





コール マネージャーは、さまざまな呼び出しにより、MCM ドライバー マネージャーの機能を呼び出します。 コール マネージャーを呼び出す**NdisCm * Xxx*** 関数、および、MCM ドライバー呼び出し**NdisMCm * Xxx*** 関数。

MCM にドライバーを呼び出しません、 **NdisCo * Xxx*** クライアントの接続指向とコール マネージャーの両方を呼び出す関数。 代わりに、MCM、ドライバーを呼び出す次同等**NdisMCm * Xxx*** 関数。

-   [**NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)の代わりに[ **NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)

-   [**NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc)の代わりに[ **NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscodeletevc)

-   [**NdisMCmOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequest)の代わりに[ **NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)

-   [**NdisMCmOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmoidrequestcomplete)の代わりに[ **NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequestcomplete)

MCM にドライバーに匹敵する呼び出しが不要[ **NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)コール マネージャーとミニポート ドライバー間の送信インターフェイスは、MCM ドライバーに内部であるため、NDIS したがって不透明になります。

 

 





