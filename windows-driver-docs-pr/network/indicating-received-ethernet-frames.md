---
title: 受信済みイーサネット フレームの表示
description: 受信済みイーサネット フレームの表示
ms.assetid: 39f35a54-1d80-4a14-b48c-2dbbfde9c86f
keywords:
- イーサネット WDK ネットワーク
- WDK ネットワークのフレーム
- イーサネットフレームの TCP/IP トランスポート (WDK ネットワーク)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9d017300abc4bfb6bcc4309e7e307bfae9e9a53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824618"
---
# <a name="indicating-received-ethernet-frames"></a>受信済みイーサネット フレームの表示





Windows TCP/IP プロトコルドライバーは、イーサネットフレームを受信するための一連の要件を定めています。 送信元のすべてのドライバーは、イーサネットフレームの表示を受け取るか、基になるドライバーの受信表示を変更する必要があります。 TCP/IP によって課せられる一般的な要件をサポートする必要があります。 これらのドライバーには、イーサネットミニポートドライバー、MUX 中間ドライバー、およびフィルタードライバーが含まれます。

**注**  ドライバーがこれらの要件に従っていない場合は、それ以降のドライバー (tcp/ip トランスポート、MUX 中間ドライバー、フィルタードライバーなど) が予期しない動作をする可能性があります。

 

イーサネットの受信通知を発信するドライバーは、次の要件をサポートする必要があります。

-   ドライバーは、受信したイーサネットフレームに対して、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を割り当てる必要があります。 各**net\_buffer\_list**構造体には、特定の用途に必要な**net\_buffer\_リスト**の**NetBufferListInfo**メンバーで定義されている帯域外 (OOB) データを含める必要があります。

-   ドライバーは、フレームに対して[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を割り当て、それを[**net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体にリンクする必要があります。 イーサネットミニポートでは、受信したデータを示すときに、net **\_buffer\_LIST**構造体に厳密に1つの**net\_バッファー**構造を割り当てる必要があります。 この制限は、イーサネットの受信パスにのみ適用されます。 ネイティブ802.11 ワイヤレス LAN インターフェイスなど、他のメディアの種類には適用されません。 または一般に NDIS。

-   NDIS 6.1 以降では、特定のシナリオで、受信したイーサネットフレームに対して、 [**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を複数のメモリ記述子リスト (mdls) に関連付けることができます。 [**Net\_buffer\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体には、1つの**net\_バッファー**構造体が含まれている必要がありますが、複数の mdls を使用すると、ドライバーは受信したパケットデータを個別のバッファーに分割できます。

    たとえば、ヘッダーデータの分割インターフェイスをサポートするイーサネットドライバーは、1つの[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に関連付けられている複数の mdls のリンクリストを使用して、受信したイーサネットフレームを分割します。 詳細については、「[ヘッダー-データの分割](header-data-split.md)」を参照してください。

    単純さとパフォーマンス上の理由から、ヘッダーデータの分割をサポートしないドライバーでは、各[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造につき1つの MDL のみを使用することを強くお勧めします。

    **注**  Windows VISTA の NDIS 6.0 では、各[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に含まれる MDL は1つだけである必要があります。

     

-   最初の MDL に、先読みサイズとして指定された NDIS のバイト数以上が含まれていない限り、IP ヘッダー、IPv4 オプション、IPsec ヘッダー、IPv6 拡張ヘッダー、または上位プロトコルヘッダーの途中で受信したイーサネットフレームを分割することはできません。

NDIS プロトコルとフィルタードライバーは、このような分割フレームが前のリスト項目で定義されている制限に準拠している場合に、受信表示の分割イーサネットフレームをサポートする必要があります。 この制限により、プロトコルとフィルタードライバーが将来の Windows バージョンと互換性があることが保証されます。

 

 





