---
title: いる CoNDIS コール マネージャーまたは MCM を閉じる
description: いる CoNDIS コール マネージャーまたは MCM を閉じる
ms.assetid: 6ef64e4c-eec4-4477-a06c-f80e21d5b1c7
keywords:
- コール マネージャーの WDK ネットワー キング、いる CoNDIS
- MCMs WDK ネットワー キング、閉じる
- 閉じる、ミニポート コール マネージャー WDK ネットワーク
- 終了呼び出しマネージャー
- ミニポート コール マネージャーを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff88c1c9a61198e9207d24ae997df85238c32e53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535922"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>いる CoNDIS コール マネージャーまたは MCM を閉じる





ときに、スタンドアロンのコール マネージャーは、基になるミニポート アダプターからバインド解除、コール マネージャーする必要がありますに通知のすべての影響を受けるいる CoNDIS クライアント関連 AF を閉じる必要があります。 各クライアントを通知するスタンドアロンの NDIS 呼び出しマネージャー、 [ **NdisCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561680)関数。

MCM を管理している CoNDIS ミニポート アダプターが停止する場合、MCM する必要がありますに通知のすべての影響を受けるクライアント関連 AF を閉じる必要があります。 MCMs 呼び出しは、各クライアントに通知する、 [ **NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546)関数。

スタンドアロンのコール マネージャーまたは MCM を呼び出す場合**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**、それぞれ、NDIS 呼び出し、 [ **ProtocolClNotifyCloseAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570234)のハンドルに関連付けられているいる CoNDIS クライアントの機能、 *NdisAfHandle*パラメーターの**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**します。 この呼び出しは、クライアントを閉じる、AF を通知します。 場合**NdisCmNotifyCloseAddressFamily**または**NdisMCmNotifyCloseAddressFamily**返します NDIS\_状態\_保留中、NDIS は呼び出しをマネージャーの[**ProtocolCmNotifyCloseAfComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570248)通知の閉じる操作の完了時に機能します。

閉じている CoNDIS クライアントで、アドレス ファミリの詳細については、[いる CoNDIS クライアントで、アドレス ファミリを閉じる](closing-an-address-family-in-a-condis-client.md)を参照してください。

 

 





