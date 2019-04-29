---
title: VMQ 送信パス
description: VMQ 送信パス
ms.assetid: a34f0708-e477-4acc-b854-f00f752be423
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdd173f2f25e2ef72373f1cc16fbbbf3e5237f2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327568"
---
# <a name="vmq-transmit-path"></a>VMQ 送信パス





上にあるドライバーを使用して送信要求の場合、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)マクロを設定する、キューに送信したデータの送信キューの識別子、 **NetBufferListFilteringInfo** OOB 情報。 **NetBufferListFilteringInfo**で指定されている、 [ **NDIS\_NET\_バッファー\_一覧\_フィルター\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff566567)構造体。

NDIS ドライバーを使用できます、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)マクロを設定またはのキューの id を取得します。[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 キューのグループに 1 つ以上の VM のキューが含まれている場合は、グループ内の VM のキューのいずれかのキューの id を送信パケットのキューの id を設定する可能性があります。

プロトコル ドライバーの設定、NDIS\_送信\_フラグ\_単一\_ビットにキュー、 *SendFlags*のパラメーター、 [ **NdisSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564535)関数があることを示すすべての送信 NET\_バッファー\_リストの構造体の呼び出しでは同じ送信キュー。

ミニポート ドライバーの設定、NDIS\_送信\_完了\_フラグ\_単一\_ビットにキュー、 *SendCompleteFlags*のパラメーター、 [ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)関数をすべて NET ことを示す\_バッファー\_呼び出しリストが同じ送信キューに送信されました。

フィルターの条件の詳細については、次を参照してください。 [VMQ フィルター操作](vmq-filter-operations.md)します。

**注**  ときに、VMQ は (たとえば、VM のライブ マイグレーション) 中に削除すると、ミニポート ドライバーを含む無効な NBL を受信する可能性があります**QueueId**値。 この場合、ミニポートする必要があります無効なキューの ID を無視して、0 (既定のキュー) を使用して、代わりにします。 **QueueId**は、 **NetBufferListFilteringInfo** 、NBL の部分の OOB のデータとを使用して取得されて、 [ **NET\_バッファー\_一覧\_受信\_キュー\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)マクロ。

 

 

 





