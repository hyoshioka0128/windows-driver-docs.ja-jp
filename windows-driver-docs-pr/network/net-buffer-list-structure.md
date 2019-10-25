---
title: NET_BUFFER_LIST 構造
description: NET_BUFFER_LIST 構造
ms.assetid: f7f19e48-cb63-458d-b175-6f99080e4cdf
keywords:
- NET_BUFFER_LIST
- ネットワークデータ WDK, 構造
- データ WDK ネットワーク, 構造
- パケット WDK ネットワーク, データ構造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec3c8bec093dcbc40cd7f70ecd49d54885f6d46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829058"
---
# <a name="net_buffer_list-structure"></a>NET\_BUFFER\_LIST 構造体





Net [ **\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体は、NET\_バッファー構造のリンクリストをパッケージ化します。

次の図は、NET\_BUFFER\_LIST 構造体のフィールドを示しています。

![net\-buffer\-list 構造内のフィールドを示す図](images/netbufferlist.png)

NET\_BUFFER\_LIST 構造体には、 **NetBufferListHeader**メンバーの[**net\_buffer\_list\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_header)構造体が含まれています。 NET\_BUFFER\_LIST\_HEADER 構造体には、 **NetBufferListData**メンバーの[**net\_buffer\_list\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_data)構造が含まれています。 NDIS マクロを使用して、NET\_BUFFER\_LIST 構造体のメンバーにアクセスする必要があります。 これらのマクロの詳細については、「 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) structure reference」ページを参照してください。

一部のメンバーは、NDIS によってのみ使用されます。 ドライバーが使用する可能性が最も高いメンバーは、次の一覧で定義されています。

<a href="" id="parentnetbufferlist"></a>**ParentNetBufferList**  
NET\_BUFFER\_LIST 構造体が親 (複製、フラグメント、または再構築) から派生した子である場合、 **ParentNetBufferList**は親の NET\_BUFFER\_LIST 構造体へのポインターを指定します。 それ以外の場合、このパラメーターは**NULL**になります。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
NET\_BUFFER\_リスト構造の割り当て元となる、NET\_BUFFER\_LIST プールを識別するプールハンドルを指定します。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
プロトコルドライバーで使用するために予約されています。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
ミニポートドライバーで使用するために予約されています。

<a href="" id="sourcehandle"></a>**SourceHandle**  
次のドライバーによって提供されるルーチンのいずれかを使用して、NDIS がバインドまたはアタッチ操作でドライバーに提供するハンドル。

<a href="" id="miniport-driver"></a>ミニポートドライバー  
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

<a href="" id="protocol-driver"></a>プロトコルドライバー  
[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

<a href="" id="filter-driver"></a>フィルタードライバー  
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

NDIS は**Sourcehandle**を使用して、NET\_BUFFER\_list 構造を送信したドライバーに、NET\_BUFFER\_list 構造体を返します。 NDIS ドライバーはこのハンドルを読み取ることができません。

<a href="" id="childrefcount"></a>**ChildRefCount**  
[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造が親 (複製、フラグメント、または再アセンブル操作によって派生した子を持つ) の場合、 **childrefcount**は既存の子の数を指定します。 それ以外の場合、このパラメーターは0になります。

<a href="" id="flags"></a>**示す**  
NET\_BUFFER\_LIST 構造体の属性を今後指定するために予約されています。 現在、ドライバーで使用できるフラグはありません。

<a href="" id="status"></a>**オンライン**  
この NET\_BUFFER\_LIST 構造体に対するネットワークデータ操作の最終的な完了ステータスを指定します。 ミニポートドライバーは、送信操作を完了する前にこの値を書き込みます。

<a href="" id="netbufferlistinfo"></a>**NetBufferListInfo**  
リスト内のすべての[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に共通する\_の一覧構造情報を、 [**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に指定します。 この情報は、"帯域外 (OOB) データ" と呼ばれることもあります。

<a href="" id="next"></a>**次に**  
NET\_BUFFER\_LIST 構造体のリンクリストにある、次の NET\_BUFFER\_LIST 構造体へのポインターを指定します。 NET\_BUFFER\_LIST 構造体がリストの最後の構造体である場合、このメンバーは**NULL**になります。

<a href="" id="firstnetbuffer"></a>**FirstNetBuffer**  
この NET\_BUFFER\_LIST 構造体に関連付けられている NET\_BUFFER 構造体のリンクリストにある、最初の NET\_バッファー構造体へのポインターを指定します。

**注**  **コンテキスト**は、 [**NET\_BUFFER\_LIST\_Context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体へのポインターです。 NDIS には、**コンテキスト**でデータを操作するためのマクロと関数が用意されています。 NET\_BUFFER\_LIST\_CONTEXT 構造体の詳細については、「 [net\_buffer\_list\_Context structure](net-buffer-list-context-structure.md)」を参照してください。

 

 

 





