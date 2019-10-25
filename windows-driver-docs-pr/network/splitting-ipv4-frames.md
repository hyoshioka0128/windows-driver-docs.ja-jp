---
title: IPv4 フレームの分割
description: IPv4 フレームの分割
ms.assetid: 1906dc31-7969-49da-adc4-8a174923d9d5
keywords:
- イーサネットフレーム分割 WDK ネットワーク、IPv4 フレーム
- IPv4 フレームの WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b49ef42c36bdf0d010679d7ca349b496c4de4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841859"
---
# <a name="splitting-ipv4-frames"></a>IPv4 フレームの分割





ヘッダーデータの分割をサポートするために、NIC は IPv4 オプションを持たない IPv4 イーサネットフレームの分割をサポートする必要があります。 NIC は、[上位層のプロトコルヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)にこのようなフレームを分割できる必要があります。

IPv4 オプションを使用した IPv4 イーサネットフレームのサポートはオプションです。 NIC は、IPv4 オプションの一部をサポートすることはできません。 NIC は、認識されない IPv4 オプションを含む IPv4 フレームを分割することはできません。 分割フレームのヘッダー部分には、IPv4 ヘッダー全体と、存在するすべての IPv4 オプションが含まれている必要があります。

NIC は、フラグメント化された IPv4 フレーム用にヘッダーデータを分割することもできます。 断片化された IPv4 フレームの詳細については、「断片化した[IP フレームの分割](splitting-fragmented-ip-frames.md)」を参照してください。

ヘッダーデータ要件のために IPv4 オプション、IPv6 拡張ヘッダー、または TCP オプションをサポートする  は、NIC が要素を認識し、その長さを決定して、ヘッダー MDL に含め、その末尾を特定できるように**することを**意味します。フレーム内の次の要素の先頭。

 

ヘッダーデータの分割プロバイダーが IPv4 フレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、 **nblflags**メンバーで\_IPv4 フラグが設定されている\_の NDIS\_NBL\_フラグが必要です。 NET\_BUFFER\_LIST 構造体でのヘッダーデータの分割フラグの設定の詳細については、「[ネットワーク\_バッファー\_リスト情報の設定](setting-net-buffer-list-information.md)」を参照してください。

追加のイーサネットフレームの特性によって、IPv4 フレームを分割する方法が決まります。 IP フレームが断片化されている場合は、「断片化した[Ip フレームの分割](splitting-fragmented-ip-frames.md)」を参照してください。 フレームに TCP 情報が含まれている場合は、「 [Tcp ペイロードでのフレームの分割](splitting-frames-at-the-tcp-payload.md)」を参照してください。 フレームに UDP 情報が含まれている場合は、「 [Udp ペイロードでのフレームの分割](splitting-frames-at-the-udp-payload.md)」を参照してください。 それ以外の場合は、「 [TCP と UDP 以外のフレームの分割](splitting-frames-other-than-tcp-and-udp.md)」を参照してください。

 

 





