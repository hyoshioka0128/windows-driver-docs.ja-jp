---
title: NET_BUFFER_LIST_CONTEXT 構造
description: NET_BUFFER_LIST_CONTEXT 構造
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
keywords:
- NET_BUFFER_LIST_CONTEXT
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
- パケット WDK ネットワーク, データ構造
- ネットワークデータ WDK、コンテキストデータ
- データ WDK ネットワーク, コンテキストデータ
- パケット WDK ネットワーク、コンテキストデータ
- コンテキストの da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83ba51f94e0b39bc8efafe76be2ea6b5f06953d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844927"
---
# <a name="net_buffer_list_context-structure"></a>NET\_BUFFER\_LIST\_CONTEXT 構造体





NDIS ドライバーは、net [ **\_buffer\_list\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を使用して、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられている追加のデータを格納します。 NET\_BUFFER\_LIST 構造体の**コンテキスト**メンバーは、NET\_BUFFER\_LIST\_context 構造体へのポインターです。 NET\_BUFFER\_LIST\_CONTEXT 構造体に格納されている情報は、スタック内の NDIS およびその他のドライバーに対して非透過的です。

次の図は、NET\_BUFFER\_LIST\_CONTEXT 構造体のフィールドを示しています。

![net\-buffer\-list\-context 構造体のフィールドを示す図](images/netbufferlistcontext.png)

[**NET\_BUFFER\_LIST\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造には、コンテキストデータを含む**contextdata**メンバーが含まれています。 このデータには、ドライバーが[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に必要とするすべてのコンテキスト情報を指定できます。

ドライバーは、次の NDIS マクロと関数を使用して、NET\_BUFFER\_LIST\_CONTEXT 構造体のメンバーにアクセスしたり操作したりする必要があります。

[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistcontext)

[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistcontext)

[**NET\_BUFFER\_LIST\_CONTEXT\_DATA\_START**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-start)

[**NET\_BUFFER\_LIST\_CONTEXT\_データ\_サイズ**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-size)

 

 





