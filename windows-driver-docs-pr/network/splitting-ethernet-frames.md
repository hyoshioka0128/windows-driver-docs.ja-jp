---
title: イーサネット フレームの分割の概要
description: イーサネット フレームの分割の概要
ms.assetid: 7b857dee-2805-4004-8f31-452f0cff0e0c
keywords:
- ヘッダー-データ分割 WDK、イーサネットフレーム分割
- イーサネットフレームの分割
- イーサネットフレーム分割 WDK ネットワーク
- イーサネットフレーム分割 WDK ネットワーク、イーサネットフレーム分割について
- ヘッダー-データ分割プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a24398a0fa413e156b5e15a4c684753bbcab08f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841867"
---
# <a name="splitting-ethernet-frames-overview"></a>イーサネット フレームの分割の概要

このセクションでは、プロバイダーが分割しているイーサネットフレームの種類に応じて、ヘッダーデータ分割プロバイダーに適用される特定のヘッダーデータの分割要件について説明します。

**注**  このトピックの一般的な要件を読み終えたら、次のトピックを使用して、各種類のイーサネットフレームの特定の要件を理解することができます。 以降のトピックでは、前のトピックの要件について説明します。 たとえば、フレームに IPv4 と UDP の情報が含まれている場合は、 [UDP ペイロード](splitting-frames-at-the-udp-payload.md)のトピックの「 [Ipv4 フレームの分割](splitting-ipv4-frames.md)とフレームの分割」を参照してください。

 

ヘッダーデータ分割プロバイダーがヘッダーデータの分割要件に対応してフレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、 **nblflags**メンバーで設定された HD\_SPLIT フラグ\_、NDIS\_NBL\_フラグが設定されている必要があります。 ヘッダーデータの分割プロバイダーでフレームが分割されない場合は、 **Nblflags**で次のフラグがクリアされた状態でフレームが示される必要があります。

-   NDIS\_NBL\_フラグ\_HD\_SPLIT

-   NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ヘッダーに分割\_

-   NDIS\_NBL\_FLAGS\_\_上位\_レイヤー\_プロトコル\_ペイロードに分割\_

ヘッダーデータを分割する方法の詳細については、「ネットワーク\_バッファー\_リストフラグとその他の受信確認要件」を参照してください。「[ヘッダーデータの分割による表示](receive-indications-with-header-data-split.md)」を参照してください。

ヘッダーデータ分割プロバイダーが、受信したフレームをヘッダーデータ分割プロバイダーの要件の外側に分割できる場合もあります。 このような場合、プロバイダーは IP ヘッダー、IPv4 オプション、IPsec ヘッダー、IPv6 拡張ヘッダー、または上位層プロトコルのヘッダーの途中でイーサネットフレームを分割しないでください。ただし、最初の MDL には、先読みサイズ。 先読みサイズの詳細については、「 [OID\_GEN\_現在の\_先読み](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-lookahead)」を参照してください。

このセクションの内容:

[IPv4 フレームの分割](splitting-ipv4-frames.md)

[IPv6 フレームの分割](splitting-ipv6-frames.md)

[断片化された IP フレームの分割](splitting-fragmented-ip-frames.md)

[上位層のプロトコルヘッダーの先頭にフレームを分割する](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)

[TCP ペイロードでフレームを分割する](splitting-frames-at-the-tcp-payload.md)

[UDP ペイロードでフレームを分割する](splitting-frames-at-the-udp-payload.md)

[TCP と UDP 以外のフレームの分割](splitting-frames-other-than-tcp-and-udp.md)

 

 





