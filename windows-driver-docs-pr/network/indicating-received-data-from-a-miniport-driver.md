---
title: ミニポート ドライバーからの受信データの表示
description: ミニポート ドライバーからの受信データの表示
ms.assetid: da5d31e9-5212-4c6c-bac2-81432a46c303
keywords:
- 受信側のデータの WDK ネットワーク
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c9d834010ef0f14b604e6ab17baec0d5a422b06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353741"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>ミニポート ドライバーからの受信データの表示





次の図に、ミニポート ドライバーを示す値を受信します。

![通知のミニポート ドライバーを示す図](images/miniportreceive.png)

ミニポート ドライバーの呼び出し、 [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)をネットワークからのデータの受信を示す関数。 **NdisMIndicateReceiveNetBufferLists**関数の指定された一覧を渡します[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体にスタックをセットアップします。上にあるドライバー。

ミニポート ドライバーが設定されている場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)、ミニポート ドライバーでの所有権を取り戻す必要があることを示します、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)すぐに構造体します。 この場合は、NDIS 呼び出しませんミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)を返す関数、 **NET\_バッファー\_一覧**構造体。 ミニポート ドライバーが所有権を得た直後後**NdisMIndicateReceiveNetBufferLists**を返します。

ミニポート ドライバーが設定されていない場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)、NDIS を返します、指定された[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造をミニポート ドライバーの[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)関数。 ミニポート ドライバーが指定された構造体の所有権を解放する NDIS が返す順序にするまでこの場合、 *MiniportReturnNetBufferLists*します。

 

 





