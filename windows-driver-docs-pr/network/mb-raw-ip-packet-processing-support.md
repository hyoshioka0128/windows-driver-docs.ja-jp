---
title: MB Raw IP パケット処理のサポート
description: MB Raw IP パケット処理のサポート
ms.assetid: 1c3327fa-1858-4247-9a18-b49d26e9a095
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54d702bc34e0e6269258d9394ae39914cba4fcda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538268"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB Raw IP パケット処理のサポート


送信/受信、データ パスの Raw IP パケットのフレームをサポートする MB ミニポート ドライバーには、次のガイドラインを確認する必要があります。

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>RAW IP パケットの処理のための net バッファー一覧 (NBL) フラグ

-   IPv4 パケットの場合。

    **NblFlags**のメンバー、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体は、NDIS に設定する必要があります\_NBL\_フラグ\_IS\_IPV4 です。

    **NetBufferListFrameType** net メンバー\_バッファー\_リスト構造は、ネットワークのバイト順で 0x0800 (Ethertype IPv4) に設定する必要があります。

-   IPv6 パケットの場合。

    **NblFlags** net メンバー\_バッファー\_リスト構造は、NDIS に設定する必要があります\_NBL\_フラグ\_IS\_IPV6 します。

    **NetBufferListFrameType** net メンバー\_バッファー\_リスト構造は、ネットワークのバイト順で 0x86dd (Ethertype IPv6) に設定する必要があります。

ミニポート ドライバーを使用できる、 [ **NdisSetNblFlag** ](https://msdn.microsoft.com/library/windows/hardware/ff564542)マクロを net バッファーの一覧にフラグを設定します。 次の行には、net バッファーの一覧で、IPv4 パケットのフラグを設定する方法を示しています。

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

ミニポート ドライバーを使用できる、 [ **NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568401)を取得し、正味のバッファーの一覧で情報を設定します。 次の行を変更する方法を示します、 **NetBufferListFrameType** IPV4 パケットのネットワーク バッファーの一覧で OOB:

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

 

 





