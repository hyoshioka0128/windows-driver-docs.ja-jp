---
title: IPv6 フレームの分割
description: IPv6 フレームの分割
ms.assetid: fe18ccfb-29d0-4b57-9308-a9d4a9c6777a
keywords:
- WDK のネットワー キング、IPv6 のフレームを分割するイーサネット フレーム
- IPv6 フレーム WDK ヘッダー以外のデータの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a1e953863e39ea35e08cde77f3424ae52e5719
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383618"
---
# <a name="splitting-ipv6-frames"></a>IPv6 フレームの分割





ヘッダー データをサポートするには、分割、NIC が IPv6 拡張ヘッダーのない分割の IPv6 イーサネット フレームをサポートする必要があります。 NIC は、上のレイヤー プロトコル ヘッダーの先頭には、このようなフレームを分割することである必要があります。

IPv6 拡張ヘッダーと IPv6 のイーサネット フレームのサポートは、省略可能です。 NIC は、IPv6 のいくつかのオプションをサポートし、他のユーザーをサポートしていません。 NIC は、IPv6 はサポートしていませんが拡張ヘッダーが含まれている IPv6 フレームを分割する必要があります。 IPv6 ヘッダー全体とすべての IPv6 拡張ヘッダーに存在する、フレームの分割のヘッダー部分を含める必要があります。

NIC には、ヘッダー データがフラグメント化された IPv6 フレームの分割もサポートできます。 断片化された IPv4 フレームの詳細については、次を参照してください。[断片化された IP パケットの分割](splitting-fragmented-ip-frames.md)します。

**注**  ヘッダー データの要件のため、IPv4 オプション、IPv6 拡張ヘッダーまたは TCP オプションをサポートしている要素を認識、その長さを決定、MDL ヘッダーに含めるのための NIC の能力を意味し、フレームの末尾と次の要素の先頭を探します。

 

ヘッダー データ プロバイダーの分割、IPv6 を分割する場合はフレームを指定された[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の有効期限があります、NDIS\_NBL\_フラグ\_IS\_IPV6 フラグの設定、 **NblFlags**メンバー。 ネット ヘッダー データ分割フラグを設定する方法については完全な\_バッファー\_構造の一覧を参照してください[設定 NET\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)します。

追加のイーサネット フレームの特徴は、IPv6 のフレームに分割する方法を決定します。 フレームが断片化されている場合は、次を参照してください。[断片化された IP パケットの分割](splitting-fragmented-ip-frames.md)します。 フレームに TCP 情報が含まれている場合は、次を参照してください。 [TCP ペイロードで分割フレーム](splitting-frames-at-the-tcp-payload.md)します。 フレームに UDP 情報が含まれている場合は、次を参照してください。 [UDP ペイロードにフレームを分割](splitting-frames-at-the-udp-payload.md)します。 その他のすべてのケースでは、次を参照してください。 [TCP 以外のフレームを分割および UDP](splitting-frames-other-than-tcp-and-udp.md)します。

 

 





