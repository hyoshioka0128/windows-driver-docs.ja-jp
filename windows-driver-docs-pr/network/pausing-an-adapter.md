---
title: アダプターの一時停止
description: アダプターの一時停止
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- ミニポート アダプタ WDK ネットワーク、一時停止
- アダプター WDK ネットワーク、一時停止
- 一時停止状態の WDK ネットワーク
- WDK のネットワークを一時停止の状態
- MiniportPause
- ミニポート アダプターが一時停止
- ミニポート アダプターが停止しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 539983513a04940149343b3867bdd8af6caa7ddc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382619"
---
# <a name="pausing-an-adapter"></a>アダプターの一時停止





NDIS ミニポート ドライバーを呼び出す[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)一時停止操作を開始する関数。 アダプターは、一時停止操作が完了するまで一時停止状態のままです。

一時停止状態では、ミニポート ドライバーを未処理に完了する必要がありますの操作を受信します。 ドライバーでは、未処理の送信操作を完了する必要がありますも、新しい送信要求を拒否する必要があります。

完了する受信操作を行うすべての呼び出しに、ドライバーが待機する、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を返す関数と NDIS は未処理のすべてに返す必要があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体、ミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。

未処理の送信操作を完了するミニポート ドライバーを呼び出す必要があります、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)関数のすべての未処理の NET\_バッファー\_リストの構造体。 ドライバーに対して行われたすべての新しい送信要求を拒否すべきその[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)すぐに機能します。

ミニポート ドライバーでは、未処理のすべての送信が完了するし、受信操作、ドライバーは、同期または非同期で一時停止要求を完了する必要があります。 ドライバーを呼び出す場合は、一時停止操作が非同期的に完了したら、 [ **NdisMPauseComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismpausecomplete)一時停止要求を完了します。 一時停止要求を完了すると、ミニポート ドライバーが一時停止状態です。

NDIS はいない停止など、他のプラグ アンド プレイ操作を開始、初期化、電源変更、または再起動操作、ミニポート ドライバーが一時停止中の状態。 NDIS は、ミニポート ドライバーは一時停止状態になった後、これらのプラグ アンド プレイ操作を開始できます。

 

 





