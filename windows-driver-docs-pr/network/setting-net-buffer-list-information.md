---
title: NET_BUFFER_LIST 情報を設定します。
description: NET_BUFFER_LIST 情報を設定します。
ms.assetid: 28f50ab4-043b-47bb-af70-e8c892288f21
keywords:
- NET_BUFFER_LIST
- ヘッダー データの分割 WDK、NET_BUFFER_LIST
- フラグ WDK ヘッダー以外のデータを分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21fecb68a1592ba9b6d4bdec6cade8658c0f6ad8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558836"
---
# <a name="setting-netbufferlist-information"></a>NET の設定\_バッファー\_情報を一覧表示





ヘッダー データの分割プロバイダーする必要がありますヘッダー データ分割にフラグを設定、 **NblFlags**のメンバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体インジケーターが表示されます。 分割のフレームの NIC をする必要がありますも提供で受信したフレームのデータ部分の物理アドレス、 **DataPhysicalAddress**のそれぞれに所属[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。

**注**  ミニポート ドライバーを設定できます、 **DataPhysicalAddress**ネットのメンバー\_場合でも、バッファーの構造、NET\_バッファーは分割フレームに関連付けられていません。 この場合、 **DataPhysicalAddress** MDL ヘッダーの物理アドレスが含まれています。

 

ヘッダー データの分割プロバイダー内のフラグを組み合わせた、 **NblFlags**ビットごとの OR 演算とメンバー。

ヘッダー データ プロバイダーの分割は、フレームを分割しない場合でも、次のフラグを設定できます。

<a href="" id="ndis-nbl-flags-is-ipv4"></a>NDIS\_NBL\_FLAGS\_IS\_IPV4  
すべてのフレームで、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) IPv4 フレームします。 このフラグが設定、NDIS 場合\_NBL\_フラグ\_IS\_IPV6 フラグを設定しない必要があります。

<a href="" id="ndis-nbl-flags-is-ipv6"></a>NDIS\_NBL\_FLAGS\_IS\_IPV6  
すべてのフレームで、NET\_バッファー\_一覧は、IPv6 フレーム。 このフラグが設定、NDIS 場合\_NBL\_フラグ\_IS\_IPV4 フラグを設定しない必要があります。

<a href="" id="ndis-nbl-flags-is-tcp"></a>NDIS\_NBL\_FLAGS\_IS\_TCP  
すべてのフレームで、NET\_バッファー\_一覧は、TCP フレーム。 このフラグが設定、NDIS 場合\_NBL\_フラグ\_IS\_UDP を設定する必要があります。 いずれかの NDIS と\_NBL\_フラグ\_IS\_IPV4 または NDIS\_NBL\_フラグ\_IS\_IPV6 を設定する必要があります。

<a href="" id="ndis-nbl-flags-is-udp"></a>NDIS\_NBL\_フラグ\_IS\_UDP  
すべてのフレームで、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388) UDP フレームします。 このフラグが設定、NDIS 場合\_NBL\_フラグ\_IS\_TCP を設定する必要があります。 いずれかの NDIS と\_NBL\_フラグ\_IS\_IPV4 または NDIS\_NBL\_フラグ\_IS\_IPV6 を設定する必要があります。

NDIS ドライバーでは、デバッグ、テスト、またはその他の目的の前のフラグを設定できます。 ドライバーがこれらのフラグを有効にしている場合、値必要があります正確に受信したフレームの内容について説明します。 これらのフラグを設定することをお勧めします。

ヘッダー データ プロバイダーを分割時に、次のヘッダー データ分割フラグを設定することができます。

<a href="" id="ndis-nbl-flags-hd-split"></a>NDIS\_NBL\_フラグ\_HD\_分割  
関連付けられているイーサネット フレームのすべてのヘッダーとデータを分割、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-header"></a>NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ヘッダー  
すべてのフレームで、NET\_バッファー\_リスト構造で分割、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。 このフラグ設定されている場合、いずれかの NDIS\_NBL\_フラグ\_IS\_IPV4 または NDIS\_NBL\_フラグ\_IS\_IPV6 を設定する必要があります。 また、いずれかの NDIS\_NBL\_フラグ\_IS\_TCP または NDIS\_NBL\_フラグ\_IS\_UDP を設定することができます。 NDIS および\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロードを設定する必要があります。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-payload"></a>NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロード  
すべてのフレームで、NET\_バッファー\_リスト構造で分割、 [TCP ペイロードの先頭](splitting-frames-at-the-tcp-payload.md)または[UDP ペイロードの先頭](splitting-frames-at-the-udp-payload.md)します。 このフラグ設定されている場合、いずれかの NDIS\_NBL\_フラグ\_IS\_IPV4 または NDIS\_NBL\_フラグ\_IS\_IPV6 を設定する必要があります。 いずれかの NDIS\_NBL\_フラグ\_IS\_TCP または NDIS\_NBL\_フラグ\_IS\_UDP を設定する必要があります。 また、NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ヘッダーを設定しない必要があります。

フラグのクリア ヘッダー データの分割プロバイダーがフレームを分割されていない場合、フレームを示す必要があります**NblFlags** :

-   NDIS\_NBL\_フラグ\_HD\_分割

-   NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ヘッダー

-   NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロード

 

 





