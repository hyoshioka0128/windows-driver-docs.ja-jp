---
title: プロトコル ドライバーからのデータの送信
description: プロトコル ドライバーからのデータの送信
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- WDK ネットワークのデータを送信します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32850e4e9c84895cd6c4de4661003ff275596c6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346784"
---
# <a name="sending-data-from-a-protocol-driver"></a>プロトコル ドライバーからのデータの送信





次の図は、プロトコル ドライバー、NDIS、およびドライバー スタック内の基になるドライバーが含まれますプロトコルのドライバーの送信操作を示しています。

![プロトコル ドライバーを示す図は、プロトコル ドライバー、ndis、およびドライバー スタック内の基になるドライバーの操作を送信します。](images/protocolsend.png)

プロトコルのドライバーの呼び出し、 [ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)関数の一覧で定義されているネットワーク データを送信する[ **NET\_バッファー\_リスト**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

プロトコル ドライバーに設定する必要があります、 **SourceHandle**各 net メンバー\_バッファー\_リスト構造体に渡されるのと同じ値を*NdisBindingHandle*パラメーター。 バインド ハンドルは、NDIS を NET を返す必要がある情報を提供します\_バッファー\_プロトコル ドライバーに基になるミニポート ドライバー呼び出しの後にリスト構造[  **。NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)します。

呼び出しの前に**NdisSendNetBufferLists**、プロトコル ドライバーの詳細情報を使用して送信要求を設定できます、 [ **NET\_バッファー\_一覧\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff568401)マクロ。 基になるドライバーは、net には、この情報を取得できます\_バッファー\_一覧\_情報マクロ。

プロトコル ドライバーを呼び出すと、すぐ**NdisSendNetBufferLists**、NET の所有権を渡し、\_バッファー\_リストの構造体と関連付けられているすべてのリソース。 NDIS 呼び出し、 [ **ProtocolSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570268)プロトコル ドライバーに構造とデータを返す関数。 NDIS は、構造体を収集でき、複数のデータは、NET のシングル リンク リストに要求を送信\_バッファー\_構造体のリストにリストを渡す前に*ProtocolSendNetBufferListsComplete*します。

NDIS 呼び出されるまで*ProtocolSendNetBufferListsComplete*プロトコルがドライバーで開始した送信の現在の状態が不明です。 プロトコル ドライバーが一時的に呼び出すときに、送信要求の割り当て済みがすべてのリソースの所有権を解放**NdisSendNetBufferLists**します。 プロトコル ドライバーが、NET の確認を試みる必要があることはありません\_バッファー\_リストの構造体、またはそのいずれかの関連データを保存 NDIS を構造体を返す前に*ProtocolSendNetBufferListsComplete*します。

*ProtocolSendNetBufferListsComplete*送信操作を完了するために必要な後処理を実行します。 ネットワーク データを送信操作が完了した送信プロトコル ドライバーを要求したなどのプロトコル ドライバーがクライアントに通知できます。

NDIS を呼び出すと*ProtocolSendNetBufferListsComplete*、プロトコル ドライバーには、すべてのネットワークに関連付けられているリソースの所有権を再度獲得\_バッファー\_によって指定されたリストの構造体*NetBufferLists*パラメーター。 *ProtocolSendNetBufferListsComplete*これらのリソースを解放できますか (呼び出すことによって、たとえば、 [ **NdisFreeNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562582)と[ **NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)) に後続の呼び出しで再利用できるように準備または**NdisSendNetBufferLists**します。

NDIS 常にデータを送信するプロトコルが指定したネットワーク プロトコルにより決定された順序で基になるミニポート ドライバーに渡されたが**NdisSendNetBufferLists**、基になるドライバーがランダムに送信要求を完了できます順序。 プロトコル ドライバーに渡されるネットワーク データを送信する NDIS にバインドされているプロトコルのすべてのドライバーできます依存は、 **NdisSendNetBufferLists**基になるドライバーを FIFO の順序で。 ただし、プロトコル ドライバーできますで使用して設定を呼び出す、基になるドライバー **NdisMSendNetBufferListsComplete**同じ順序で。

 

 





