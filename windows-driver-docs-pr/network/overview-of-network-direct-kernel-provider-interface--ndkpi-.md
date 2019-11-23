---
title: Network Direct Kernel Provider Interface (NDKPI) の概要
description: このセクションでは、ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI) の概要について説明します。
ms.assetid: D9667238-FD2E-44DE-920F-FA4CF3365D93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 796de16650f03bda40e06670185c168bf804b5c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843729"
---
# <a name="overview-of-network-direct-kernel-provider-interface-ndkpi"></a>Network Direct Kernel Provider Interface (NDKPI) の概要


ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI) は、ネットワークアダプター (RNIC とも呼ばれます) でのカーネルモードのリモートダイレクトメモリアクセス (RDMA) のサポートを Ihv が提供できるようにする、NDIS の拡張機能です。 アダプターの RDMA 機能を公開するには、IHV が[Ndkpi リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)で定義されているように、ndkpi インターフェイスを実装する必要があります。

-   [NDKPI と RDMA](#ndkpi-and-rdma)
-   [NDK プロバイダー](#the-ndk-provider)
-   [NDK コンシューマー](#the-ndk-consumer)

### <a name="ndkpi-and-rdma"></a>NDKPI と RDMA

NIC ベンダは、ソフトウェア、ファームウェア、およびハードウェアの組み合わせとして RDMA を実装します。 ハードウェアとファームウェアの部分は、NDK/RDMA 機能を提供するネットワークアダプターです。 この種類のアダプタは、RDMA 対応の NIC (RNIC) とも呼ばれます。 ソフトウェア部分は、NDKPI インターフェイスを実装する NDK 対応ミニポートドライバーです。

RDMA の Windows 実装はネットワークダイレクト (ND) と呼ばれます。 カーネルの部分は、ネットワークダイレクトカーネル (NDK) と呼ばれます。

NDK プロバイダーは、NDK 対応のミニポートアダプターに割り当てられた IPv4 アドレスと IPv6 アドレスの両方を使用したネットワーク直接接続をサポートしている必要があります。

RDMA の詳細については、「 [rdma のバックグラウンド読み取り](background-reading-on-rdma.md)」を参照してください。

### <a name="the-ndk-provider"></a>NDK プロバイダー

NDK プロバイダーは、NDKPI インターフェイスを実装するミニポートドライバーです。

NDK プロバイダーは、PnP マネージャーによって読み込まれ、初期化されます。 詳細については、「 [Ndk 対応ミニポートドライバーの初期化](initializing-an-ndk-capable-miniport-driver.md)」および「 [Ndk ミニポートアダプターの初期化](initializing-an-ndk-miniport-adapter.md)」を参照してください。

NDK プロバイダーが読み込まれ初期化されると、NDK コンシューマーからの要求を処理する準備が整います。 これらの要求は、プロバイダー関数への呼び出しとして受信されます。

NDK コンシューマーからの要求を処理する場合、プロバイダーは、コンシューマーの NDK コールバック関数を呼び出すことができます。 これらは、 [Ndkpi コンシューマーコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)に記載されています。

NDK プロバイダーは、ndkpi[リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)に記載されている ndkpi インターフェイスのすべての要素を実装する必要があります。ただし、 [Ndkpi コンシューマーコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は除きます。

### <a name="the-ndk-consumer"></a>NDK コンシューマー

NDK コンシューマーは、SMB サーバーやクライアントなどのカーネルモードの Windows コンポーネントです。

**注**  このドキュメントでは、NDK コンシューマーの実装方法については説明しません。 NDKPI コンシューマーデバイスドライバーインターフェイス (DDI) は、独自の Windows 内部インターフェイスです。

 

NDK コンシューマーは、プロバイダーの*Ndkopenadapter* ([*OPEN\_NDK\_adapter\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)) コールバック関数を呼び出して、アダプターオブジェクトと*ndkopenadapter* ([*ndk\_FN\_close\_object*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_object)) を作成して閉じます。 プロバイダーがアダプターオブジェクトを作成すると、コンシューマーは他のプロバイダーコールバック関数を呼び出して、追加の NDK オブジェクトを作成します。

NDK コンシューマーは、NDK プロバイダーによって呼び出される[Ndkpi コンシューマーコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)を実装します。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






