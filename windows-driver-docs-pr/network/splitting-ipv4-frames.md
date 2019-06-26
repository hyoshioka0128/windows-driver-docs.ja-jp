---
title: IPv4 フレームの分割
description: IPv4 フレームの分割
ms.assetid: 1906dc31-7969-49da-adc4-8a174923d9d5
keywords:
- WDK のネットワー キング、IPv4 のフレームを分割するイーサネット フレーム
- IPv4 フレーム WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b59aa08c01876ea02b8559ccc0670fe2805e6232
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383612"
---
# <a name="splitting-ipv4-frames"></a>IPv4 フレームの分割





ヘッダー データをサポートするには、分割、NIC は、IPv4 のオプションがない分割の IPv4 イーサネット フレームをサポートする必要があります。 NIC では、このようなフレームを分割できる必要があります、[レイヤー プロトコルの上限ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。

IPv4 のオプションを使用して IPv4 イーサネット フレームのサポートは、省略可能です。 IPv4 のいくつかのオプションとは、NIC をサポートできます。 NIC が不明 IPv4 オプションを含む IPv4 フレームを分割する必要があります。 フレームの分割のヘッダー部分は、全体の IPv4 ヘッダーとそのすべての IPv4 オプションが存在するを含める必要があります。

NIC には、ヘッダー データの断片化された IPv4 フレームの分割もサポートできます。 断片化された IPv4 フレームの詳細については、次を参照してください。[断片化された IP パケットの分割](splitting-fragmented-ip-frames.md)します。

**注**  ヘッダー データの要件のため、IPv4 オプション、IPv6 拡張ヘッダーまたは TCP オプションをサポートしている要素を認識、その長さを決定、MDL ヘッダーに含めるのための NIC の能力を意味し、フレームの末尾と次の要素の先頭を探します。

 

ヘッダー データ プロバイダーの分割、IPv4 を分割する場合はフレームを指定された[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の有効期限があります、NDIS\_NBL\_フラグ\_IS\_IPV4 フラグの値設定、 **NblFlags**メンバー。 ネット ヘッダー データ分割フラグを設定する方法については完全な\_バッファー\_構造の一覧を参照してください[設定 NET\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)します。

追加のイーサネット フレームの特徴は、IPv4 のフレームに分割する方法を決定します。 IP のフレームが断片化されている場合は、次を参照してください。[断片化された IP パケットの分割](splitting-fragmented-ip-frames.md)します。 フレームに TCP 情報が含まれている場合は、次を参照してください。 [TCP ペイロードで分割フレーム](splitting-frames-at-the-tcp-payload.md)します。 フレームに UDP 情報が含まれている場合は、次を参照してください。 [UDP ペイロードにフレームを分割](splitting-frames-at-the-udp-payload.md)します。 その他のすべてのケースでは、次を参照してください。 [TCP 以外のフレームを分割および UDP](splitting-frames-other-than-tcp-and-udp.md)します。

 

 





