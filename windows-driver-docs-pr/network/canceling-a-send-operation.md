---
title: 送信操作のキャンセル
description: 送信操作のキャンセル
ms.assetid: 5bd7a815-4e4d-4259-b322-f4f8d07f2e1a
keywords:
- ネットワーク、WDK のデータを送信します。
- WDK のデータ ネットワーク、送信します。
- WDK のパケットを送信するネットワークを
- WDK ネットワークのデータを送信します。
- NDIS_SET_NET_BUFFER_LIST_CANCEL_ID
- 送信操作の WDK ネットワー キングのキャンセル
- キャンセル Id WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fa24eceedc606034b880484bd119faa56494981
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570397"
---
# <a name="canceling-a-send-operation"></a>送信操作のキャンセル





次の図は、送信操作の取り消しを示します。

![送信操作のキャンセルを示す図](images/netbuffercancelsend.png)

ドライバーを呼び出し、 [ **NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff567299)各用のマクロ[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)伝送の下位レベルのドライバーに渡される構造体。 NDIS\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID 関数は、キャンセルの識別子を持つ指定されたパケットをマークします。

パケットにキャンセル Id を割り当てる前に、ドライバーを呼び出す必要があります[ **NdisGeneratePartialCancelId** ](https://msdn.microsoft.com/library/windows/hardware/ff562623)各キャンセル ID を割り当てることの高位のバイトを取得します。 これにより、ドライバーに取り消しシステム内の他のドライバーによって割り当てられた Id が重複していないこと。 ドライバーを呼び出す通常**NdisGeneratePartialCancelId**から 1 回、 **DriverEntry**ルーチンは呼び出すことで、ドライバーが 1 つ以上の部分取り消し識別子を取得するただし、 **NdisGeneratePartialCancelId** 2 回以上。

マークされたネットワーク内のデータの保留中の転送をキャンセルする\_バッファー\_リスト構造では、ドライバーにキャンセル ID に渡す、 [ **NdisCancelSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561623)関数。 ドライバーとして使用できるは、NET\_バッファー\_リスト構造体のキャンセルの ID を呼び出して、 [ **NDIS\_取得\_NET\_バッファー\_一覧\_キャンセル\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff565683)マクロ。

場合、ドライバーはすべて[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)同じキャンセル識別子を持つ構造体、を単一の呼び出しで伝送保留中のすべてキャンセルことできます**NdisCancelSendNetBufferLists**します。 場合、ドライバーはすべて NET\_バッファー\_NET のサブグループ リスト構造\_バッファー\_リストの一意の識別子を持つ構造体、保留中のすべての単一の呼び出しでは、そのサブグループ内で伝送キャンセルができます**NdisCancelSendNetBufferLists**します。

NDIS 呼び出し、 [ *MiniportCancelSend* ](https://msdn.microsoft.com/library/windows/hardware/ff559342)バインドで適切な下位レベルのドライバーの機能です。 保留中の転送を中止後、基になるミニポート ドライバーを呼び出して、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)を NET を返す関数\_バッファー\_一覧構造体と NDIS の完了ステータス\_状態\_送信\_中止されました。 NDIS、さらに、適切なドライバーの[ **ProtocolSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570268)関数。

その*ProtocolSendNetBufferListsComplete*関数の場合、プロトコル ドライバーには、NDIS が呼び出すことができます\_設定\_NET\_バッファー\_一覧\_キャンセル\_ID*CancelId*設定**NULL**します。 これにより、NET\_バッファー\_から古いキャンセル ID に置き換えますもう一度使用されている誤って一覧。

 

 





