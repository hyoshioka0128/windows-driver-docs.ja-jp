---
title: MB Raw IP パケット処理のサポート
description: MB Raw IP パケット処理のサポート
ms.assetid: 1c3327fa-1858-4247-9a18-b49d26e9a095
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb2db92922af73fdd697becb2ae4aff4efd55a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844274"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB Raw IP パケット処理のサポート


送信/受信データパスの未加工の IP パケットフレームをサポートする MB のミニポートドライバーは、次のガイドラインを確認する必要があります。

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>未加工 IP パケット処理のための Net buffer list (NBL) フラグ

-   IPv4 パケットの場合:

    [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**nblflags**メンバーを NDIS\_NBL\_FLAGS\_IPV4 に設定する必要があります。

    NET\_BUFFER\_LIST 構造体の**NetBufferListFrameType**メンバーは、ネットワークのバイト順で 0X0800 (Ethertype IPv4) に設定する必要があります。

-   IPv6 パケットの場合:

    NET\_BUFFER\_LIST 構造体の**Nblflags**メンバーを NDIS\_NBL\_FLAGS\_IPV6 に設定する必要があります。

    NET\_BUFFER\_LIST 構造体の**NetBufferListFrameType**メンバーは、ネットワークのバイト順で 0x86dd (Ethertype IPv6) に設定する必要があります。

ミニポートドライバーでは、 [**NdisSetNblFlag**](https://docs.microsoft.com/windows-hardware/drivers/network/ndissetnblflag)マクロを使用して、net バッファー一覧にフラグを設定できます。 次の行は、net buffer リストで IPv4 パケットフラグを設定する方法を示しています。

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

ミニポートドライバーでは、net [ **\_buffer\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)を使用して、net バッファー一覧の情報を取得および設定できます。 次の行は、IPV4 パケットのネットワークバッファー一覧の**NetBufferListFrameType** OOB を変更する方法を示しています。

```C++
Value = ConvertToNetworkByteOrder(0x0800);
```

```C++
NET_BUFFER_LIST_INFO(pNbl, NetBufferListFrameType) = Value;
```

### <a name="send-path-processing"></a>送信パスの処理

MB サービスは、ネットワーク経由で送信するためにリストをミニポートドライバーに渡す前に、これらのフラグを NBL に設定します。 ミニポートドライバーは、入力 NBL のフラグを確認できます。

### <a name="receive-path-processing"></a>受信パスの処理

ミニポートドライバーは、受信パケットの NBL を MB サービスに渡す前に、NBL でフラグを設定する必要があります。

ミニポートドライバーがドライバーの開発フェーズ中に未加工の IP パケット処理を実装していても、DHCP サーバーのスプーフィングが有効になっている場合 (EnableDhcp = 1)、ミニポートドライバーは次のことを確認する必要があります。

-   ミニポートドライバーからの DHCP 応答で設定されたハードウェアアドレスとその長さは、NDIS\_ミニポート\_アダプターのミニポートドライバーによって指定される**Currentmacaddress**および**macaddresslength**の値と一致している必要があります。一般\_属性構造\_ます。

-   ミニポートドライバーからの DHCP 応答のトランザクション ID ( **xid**メンバー) は、クライアントからの dhcp 要求メッセージに設定されたトランザクション id と完全に一致する必要があります。

 

 





