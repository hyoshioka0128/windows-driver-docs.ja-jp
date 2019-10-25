---
title: ネットワーク ドライバーの非同期 I/O と補完関数
description: ネットワーク ドライバーの非同期 I/O と補完関数
ms.assetid: fbb940d8-41ad-4f66-998b-f5dc829b54cc
keywords:
- ネットワークドライバー WDK、非同期操作
- 非同期 i/o WDK ネットワーク
- 完了関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 031cb7ae49de744ee72c7b842296b4d5df1576a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838225"
---
# <a name="asynchronous-io-and-completion-functions-in-network-drivers"></a>ネットワーク ドライバーの非同期 I/O と補完関数





待機時間は、一部のネットワーク操作に固有のものです。 この待機時間が原因で、ミニポートドライバーによって提供されるトップエッジ関数の多くとプロトコルドライバーの下位機能は、非同期操作をサポートするように設計されています。 時間のかかるタスクが完了するまで、またはハードウェアイベントを通知するために、ループ内で待機している CPU サイクルを無駄にするのではなく、ネットワークドライバーはほとんどの操作を非同期に処理する機能に依存します。

非同期ネットワーク i/o は、*完了*関数を使用してサポートされています。 次の例では、ネットワーク*送信*操作の完了関数を使用する方法を示していますが、このメカニズムは、プロトコルまたはミニポートドライバーによって実行される他の多くの操作にも存在します。

プロトコルドライバーが NDIS を呼び出してパケットを送信するときに、ミニポートドライバーの[*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数が呼び出されると、ミニポートドライバーはこの要求を直ちに完了し、結果として適切な状態の値を返すことができます。 同期操作では、送信、NDIS\_ステータス\_リソース、および何らかのエラーが発生したことを示す NDIS\_STATUS\_のエラーが正常に完了した場合に発生する可能性のある応答として、NDIS\_の状態を\_ます。

ただし、送信操作の完了には時間がかかることがありますが、ミニポートドライバー (または NDIS) はパケットをキューに置いて、NIC が送信操作の結果を示すまで待機します。 ミニポートドライバーの*Miniportsendnetbufferlists*関数は、NDIS\_STATUS\_PENDING の状態値を返すことによって、この操作を非同期的に処理できます。 ミニポートドライバーは送信操作を完了すると、完了関数[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出し、送信されたパケット記述子へのポインターを渡します。 この情報は、プロトコルドライバーに渡され、シグナリングが完了します。

ほとんどのドライバー操作は、同様の完了関数を使用した非同期操作のサポートを完了するために長い時間が必要になる場合があります。 このような関数には、 **Ndism*Xxx*** という形式の名前が付いています。

次のような完了関数も用意されています。

-   構成を設定し、クエリを実行します。

-   ハードウェアをリセットします。

-   状態を示します。

-   受信したデータを示します。

-   受信したデータを転送します。

 

 





