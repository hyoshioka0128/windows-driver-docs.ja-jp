---
title: NET_BUFFER_LIST 情報の設定
description: NET_BUFFER_LIST 情報の設定
ms.assetid: 28f50ab4-043b-47bb-af70-e8c892288f21
keywords:
- NET_BUFFER_LIST
- ヘッダー-データ分割 WDK、NET_BUFFER_LIST
- WDK ヘッダーのフラグ-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54e4cdf46502759da1b7d87bfd7f44179ba6e193
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841938"
---
# <a name="setting-net_buffer_list-information"></a>ネットワーク\_バッファー\_リスト情報を設定しています





ヘッダーデータの分割プロバイダーは、受信表示のために、 [**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の**nblflags**メンバーにヘッダーデータ分割フラグを設定する必要があります。 分割フレームの場合、NIC は、各[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の**DataPhysicalAddress**メンバーの受信フレームのデータ部分の物理アドレスも指定する必要があります。

ネットワーク\_バッファーが分割フレームに関連付けられていない場合でも、ミニポート**ドライバー  net**\_バッファー構造の**DataPhysicalAddress**メンバーを設定できます。 この場合、 **DataPhysicalAddress**にはヘッダー MDL の物理アドレスが含まれます。

 

ヘッダーデータ分割プロバイダーは、 **Nblflags**メンバーのフラグをビットごとの or 演算に結合します。

フレームが分割されていない場合でも、ヘッダーデータ分割プロバイダーは次のフラグを設定できます。

<a href="" id="ndis-nbl-flags-is-ipv4"></a>NDIS\_NBL\_フラグ\_は IPV4\_  
[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)内のすべてのフレームは、IPv4 フレームです。 このフラグが設定されている場合は\_IPV6 フラグを設定することはできませんが、NDIS\_NBL\_FLAGS\_になります。

<a href="" id="ndis-nbl-flags-is-ipv6"></a>NDIS\_NBL\_FLAGS\_は IPV6\_  
NET\_BUFFER\_リスト内のすべてのフレームは、IPv6 フレームです。 このフラグが設定されている場合、NDIS\_NBL\_FLAGS\_は\_IPV4 フラグを設定することはできません。

<a href="" id="ndis-nbl-flags-is-tcp"></a>NDIS\_NBL\_FLAGS\_が TCP\_  
NET\_BUFFER\_リスト内のすべてのフレームが TCP フレームです。 このフラグが設定されている場合、NDIS\_NBL\_FLAGS\_は\_UDP を設定することはできません。 また、NDIS\_NBL\_FLAGS\_は\_IPV4 または NDIS\_NBL\_フラグ\_IPV6\_設定する必要があります。

<a href="" id="ndis-nbl-flags-is-udp"></a>NDIS\_NBL\_FLAGS\_が UDP\_  
[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)内のすべてのフレームは、UDP フレームです。 このフラグが設定されている場合、NDIS\_NBL\_FLAGS\_は\_TCP を設定することはできません。 また、NDIS\_NBL\_FLAGS\_は\_IPV4 または NDIS\_NBL\_フラグ\_IPV6\_設定する必要があります。

すべての NDIS ドライバーは、デバッグやテストなどの目的で、上記のフラグを設定できます。 ドライバーでこれらのフラグが設定されている場合、値は受信フレームの内容を正確に記述する必要があります。 これらのフラグを設定することをお勧めします。

ヘッダーデータ分割プロバイダーは、次のヘッダーデータ分割フラグを設定できます。

<a href="" id="ndis-nbl-flags-hd-split"></a>NDIS\_NBL\_フラグ\_HD\_SPLIT  
ヘッダーとデータは、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられているすべてのイーサネットフレームに分割されます。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-header"></a>NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ヘッダーに分割\_  
NET\_BUFFER\_LIST 構造体のすべてのフレームは、[上位層のプロトコルヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)に分割されます。 このフラグが設定されている場合、NDIS\_NBL\_FLAGS\_は\_IPV4 または NDIS\_NBL\_フラグ\_IPV6 を設定する必要があります。 また、NDIS\_NBL\_FLAGS\_は\_TCP または NDIS\_NBL\_フラグ\_\_UDP を設定できます。 および NDIS\_NBL\_FLAGS\_\_上位\_レイヤーでの分割\_\_プロトコル\_ペイロードを設定することはできません。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-payload"></a>NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ペイロードに分割\_  
NET\_BUFFER\_LIST 構造体のすべてのフレームは、 [TCP ペイロードの開始](splitting-frames-at-the-tcp-payload.md)時または[UDP ペイロードの開始](splitting-frames-at-the-udp-payload.md)時に分割されます。 このフラグが設定されている場合、NDIS\_NBL\_FLAGS\_は\_IPV4 または NDIS\_NBL\_フラグ\_IPV6 を設定する必要があります。 NDIS\_NBL\_FLAGS\_は\_TCP または NDIS\_NBL\_フラグ\_\_UDP を設定する必要があります。 また、NDIS\_NBL\_FLAGS\_\_分割され\_上位\_レイヤーで\_プロトコル\_ヘッダーを設定することはできません。

ヘッダーデータの分割プロバイダーでフレームが分割されない場合は、 **Nblflags**で次のフラグがクリアされた状態でフレームが示される必要があります。

-   NDIS\_NBL\_フラグ\_HD\_SPLIT

-   NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ヘッダーに分割\_

-   NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ペイロードに分割\_

 

 





