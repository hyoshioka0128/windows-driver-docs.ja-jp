---
title: IPv6 フレームの分割
description: IPv6 フレームの分割
ms.assetid: fe18ccfb-29d0-4b57-9308-a9d4a9c6777a
keywords:
- イーサネットフレーム分割 WDK ネットワーク、IPv6 フレーム
- IPv6 フレーム WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7527df846b70113243a764ded53ca42bbd153300
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841860"
---
# <a name="splitting-ipv6-frames"></a>IPv6 フレームの分割





ヘッダーデータの分割をサポートするには、NIC が ipv6 拡張ヘッダーを使用せずに IPv6 イーサネットフレームの分割をサポートする必要があります。 NIC は、上位層のプロトコルヘッダーの先頭にこのようなフレームを分割できる必要があります。

Ipv6 拡張ヘッダーを使用した IPv6 イーサネットフレームのサポートはオプションです。 NIC は、IPv6 オプションをサポートしておらず、他のオプションをサポートしていません。 NIC は、でサポートされていない IPv6 拡張ヘッダーを含む IPv6 フレームを分割することはできません。 分割フレームのヘッダー部分には、IPv6 ヘッダー全体および存在するすべての IPv6 拡張ヘッダーが含まれている必要があります。

NIC は、フラグメント化された IPv6 フレーム用にヘッダーデータを分割することもできます。 断片化された IPv4 フレームの詳細については、「断片化した[IP フレームの分割](splitting-fragmented-ip-frames.md)」を参照してください。

ヘッダーデータ要件のために IPv4 オプション、IPv6 拡張ヘッダー、または TCP オプションをサポートする  は、NIC が要素を認識し、その長さを決定して、ヘッダー MDL に含め、その末尾を特定できるように**することを**意味します。フレーム内の次の要素の先頭。

 

ヘッダーデータ分割プロバイダーが IPv6 フレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、 **nblflags**メンバーで設定され\_IPv6 フラグが設定されている\_の NDIS\_NBL\_フラグが必要です。 NET\_BUFFER\_LIST 構造体でのヘッダーデータの分割フラグの設定の詳細については、「[ネットワーク\_バッファー\_リスト情報の設定](setting-net-buffer-list-information.md)」を参照してください。

追加のイーサネットフレームの特性によって、IPv6 フレームを分割する方法が決まります。 フレームが断片化されている場合は、「断片化した[IP フレームの分割](splitting-fragmented-ip-frames.md)」を参照してください。 フレームに TCP 情報が含まれている場合は、「 [Tcp ペイロードでのフレームの分割](splitting-frames-at-the-tcp-payload.md)」を参照してください。 フレームに UDP 情報が含まれている場合は、「 [Udp ペイロードでのフレームの分割](splitting-frames-at-the-udp-payload.md)」を参照してください。 それ以外の場合は、「 [TCP と UDP 以外のフレームの分割](splitting-frames-other-than-tcp-and-udp.md)」を参照してください。

 

 





