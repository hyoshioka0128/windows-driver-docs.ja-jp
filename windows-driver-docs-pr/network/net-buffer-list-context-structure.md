---
title: NET_BUFFER_LIST_CONTEXT 構造
description: NET_BUFFER_LIST_CONTEXT 構造
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
keywords:
- NET_BUFFER_LIST_CONTEXT
- ネットワーク データ WDK、構造体
- ネットワー キング WDK データ、構造体
- パケットの WDK ネットワーク、データ構造体
- データ コンテキスト データ、WDK をネットワークします。
- データの WDK ネットワー キング、コンテキスト データ
- コンテキスト データ、パケットの WDK ネットワーク
- コンテキスト da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8207ac2cd172ca4cb75cc216e5bbdc91f09a53ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379765"
---
# <a name="netbufferlistcontext-structure"></a>NET\_バッファー\_一覧\_CONTEXT 構造体





NDIS ドライバーを使用して、 [ **NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)に関連付けられている追加のデータを格納する構造体、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 **コンテキスト**net メンバー\_バッファー\_リスト構造は、NET へのポインター\_バッファー\_一覧\_CONTEXT 構造体。 NET に格納された情報\_バッファー\_一覧\_CONTEXT 構造体は、NDIS とスタックの他のドライバーに対して非透過的です。

次の図は、NET でフィールドを示します\_バッファー\_一覧\_CONTEXT 構造体。

![net のフィールドを示す図\-バッファー\-一覧\-context 構造体](images/netbufferlistcontext.png)

[ **NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造が含まれます**ContextData**コンテキスト データが含まれるメンバー。 このデータをドライバーが必要とするコンテキスト情報を指定できます、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

ドライバーがアクセスして、NET 内のメンバーを操作する次の NDIS マクロと関数を使用する必要があります\_バッファー\_一覧\_CONTEXT 構造体。

[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistcontext)

[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistcontext)

[**NET\_バッファー\_一覧\_コンテキスト\_データ\_開始**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-start)

[**NET\_バッファー\_一覧\_コンテキスト\_データ\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-size)

 

 





