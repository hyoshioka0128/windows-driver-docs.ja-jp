---
title: MB Raw IP パケット処理のサポート
description: MB Raw IP パケット処理のサポート
ms.assetid: 1c3327fa-1858-4247-9a18-b49d26e9a095
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0bbe7a81c027247557cd66b9d749e4ccae03413
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374022"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB Raw IP パケット処理のサポート


送信/受信、データ パスの Raw IP パケットのフレームをサポートする MB ミニポート ドライバーには、次のガイドラインを確認する必要があります。

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>RAW IP パケットの処理のための net バッファー一覧 (NBL) フラグ

-   IPv4 パケットの場合。

    **NblFlags**のメンバー、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体は、NDIS に設定する必要があります\_NBL\_フラグ\_IS\_IPV4 です。

    **NetBufferListFrameType** net メンバー\_バッファー\_リスト構造は、ネットワークのバイト順で 0x0800 (Ethertype IPv4) に設定する必要があります。

-   IPv6 パケットの場合。

    **NblFlags** net メンバー\_バッファー\_リスト構造は、NDIS に設定する必要があります\_NBL\_フラグ\_IS\_IPV6 します。

    **NetBufferListFrameType** net メンバー\_バッファー\_リスト構造は、ネットワークのバイト順で 0x86dd (Ethertype IPv6) に設定する必要があります。

ミニポート ドライバーを使用できる、 [ **NdisSetNblFlag** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndissetnblflag)マクロを net バッファーの一覧にフラグを設定します。 次の行には、net バッファーの一覧で、IPv4 パケットのフラグを設定する方法を示しています。

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

ミニポート ドライバーを使用できる、 [ **NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)を取得し、正味のバッファーの一覧で情報を設定します。 次の行を変更する方法を示します、 **NetBufferListFrameType** IPV4 パケットのネットワーク バッファーの一覧で OOB:

```C++
Value = ConvertToNetworkByteOrder(0x0800);
```

```C++
NET_BUFFER_LIST_INFO(pNbl, NetBufferListFrameType) = Value;
```

### <a name="send-path-processing"></a>パスの処理を送信します。

MB サービスに、一覧をネットワーク経由で送信するミニポート ドライバーに渡す前に、NBL でこれらのフラグを設定します。 ミニポート ドライバーでは、入力 NBL のフラグを確認できます。

### <a name="receive-path-processing"></a>受信パスの処理

ミニポート ドライバーは、NBL を受信したパケットの MB サービスに渡す前に、NBL でフラグを設定する必要があります。

ミニポート ドライバーで Raw IP パケットの処理を実装、ドライバーの開発フェーズ中が引き続き有効が DHCP サーバー スプーフィング (EnableDhcp = 1)、ミニポート ドライバーを確認してください以下。

-   ハードウェア アドレスとその長さが、ミニポート ドライバーからの応答を DHCP 設定の値に一致する必要があります、 **CurrentMacAddress**と**MacAddressLength**のミニポート ドライバーで指定されたメンバー、NDIS\_ミニポート\_アダプター\_全般\_属性の構造体。

-   トランザクション ID (、 **xid**メンバー) ドライバー ミニポートから DHCP 応答の DHCP 要求メッセージの設定、クライアントからトランザクション ID 正確に一致する必要があります。

 

 





