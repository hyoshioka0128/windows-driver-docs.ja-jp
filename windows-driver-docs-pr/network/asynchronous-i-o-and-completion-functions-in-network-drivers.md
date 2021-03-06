---
title: ネットワーク ドライバーの非同期 I/O と補完関数
description: ネットワーク ドライバーの非同期 I/O と補完関数
ms.assetid: fbb940d8-41ad-4f66-998b-f5dc829b54cc
keywords:
- ネットワーク ドライバー WDK、非同期操作
- 非同期の I/O WDK ネットワーク
- 完了関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 078bc15a489bb0c7edac4b335d08026942d2911c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384412"
---
# <a name="asynchronous-io-and-completion-functions-in-network-drivers"></a>ネットワーク ドライバーの非同期 I/O と補完関数





待機時間は、一部のネットワーク操作に固有です。 この待機時間のため、非同期操作をサポートするために多くのミニポート ドライバーとプロトコル ドライバーの下位 edge 関数によって提供される上端関数が設計されています。 CPU の無駄ではなく、いくつかの時間のかかるタスクが終了するか、通知、ネットワーク ドライバーは、ほとんどの操作を非同期的に処理する機能に依存するハードウェア イベントのループで待機しているサイクルです。

使用して非同期ネットワーク I/O がサポートされている、*完了*関数。 次の例のネットワーク完了関数を使用して*送信*プロトコルまたはミニポート ドライバーで実行されるその他の多くの操作の操作が同じメカニズムが存在します。

プロトコル ドライバーがパケットを送信する NDIS を呼び出すと、ミニポート ドライバーの呼び出しで結果[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)関数、ミニポート ドライバーはすぐにこの要求を完了するとことができますその結果、適切な状態の値を返します。 回答の候補は、同期操作は、NDIS\_状態\_NDIS、送信が正常に完了の成功を\_状態\_リソース、および NDIS\_状態\_エラー何らかのエラーを示すです。

送信操作がパケットと送信操作の結果を示すために NIC の間、待機キューの中に、ミニポート ドライバー (NDIS) 完了に時間がかかることができます。 ミニポート ドライバー *MiniportSendNetBufferLists*関数は NDIS のステータス値を返すことによってこの操作を非同期的に処理できる\_状態\_保留します。 完了関数を呼び出し、ミニポート ドライバーでは、送信操作が完了したら、 [ **NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)、送信されたパケット記述子へのポインターを渡します。 この情報は、完了の通知、プロトコル ドライバーに渡されます。

同様の入力候補機能でサポートの非同期操作を完了に時間がかかることが必要とするほとんどのドライバー操作。 このような関数は、フォームの名前を持つ**NdisM*Xxx*完了**します。

入力候補の関数にも用意されています。

-   設定とクエリの構成。

-   ハードウェアをリセットします。

-   状態を示します。

-   受信したデータを示します。

-   受信したデータを転送します。

 

 





