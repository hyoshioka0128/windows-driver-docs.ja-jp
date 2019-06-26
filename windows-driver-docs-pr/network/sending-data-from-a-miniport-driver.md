---
title: ミニポート ドライバーからのデータの送信
description: ミニポート ドライバーからのデータの送信
ms.assetid: f82475ff-8d32-4448-9b19-b6fa97a93d32
keywords:
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e58ecc34baa7cf7333a8e7c4e8c5a80ddbb9d4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381189"
---
# <a name="sending-data-from-a-miniport-driver"></a>ミニポート ドライバーからのデータの送信





次の図は、ミニポート ドライバーの送信操作を示しています。

![送信操作のミニポート ドライバーを示す図](images/miniportsend.png)

NDIS ミニポート ドライバーを呼び出す[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)のリンク リストによって定義されたネットワーク データを送信する関数[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

ミニポート ドライバーの呼び出し、 [ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete) NET のリンクの一覧を返す関数\_バッファー\_構造体のリストを返すと、上にあるドライバーには送信要求の最終的な状態です。

 

 





