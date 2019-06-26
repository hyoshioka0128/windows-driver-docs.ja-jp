---
title: Network Direct Kernel Provider Interface (NDKPI) の概要
description: このセクションでは、概要のネットワーク直接カーネル プロバイダー インターフェイス (NDKPI) を提供します。
ms.assetid: D9667238-FD2E-44DE-920F-FA4CF3365D93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 028b126224c08f2fcdf75143de695750ad2e459d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384373"
---
# <a name="overview-of-network-direct-kernel-provider-interface-ndkpi"></a>Network Direct Kernel Provider Interface (NDKPI) の概要


ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI) では、NDIS Ihv (、RNIC とも呼ばれます) のネットワーク アダプターでのカーネル モード リモート ダイレクト メモリ アクセス (RDMA) のサポートを提供することができる拡張機能です。 アダプターの RDMA 機能を公開する、IHV する必要がありますインターフェイスを実装、NDKPI で定義されている、 [NDKPI 参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

-   [NDKPI と RDMA の場合](#ndkpi-and-rdma)
-   [NDK プロバイダー](#the-ndk-provider)
-   [NDK コンシューマー](#the-ndk-consumer)

### <a name="ndkpi-and-rdma"></a>NDKPI と RDMA の場合

NIC ベンダーは、ソフトウェア、ファームウェア、およびハードウェアの組み合わせで RDMA を実装します。 ハードウェアおよびファームウェアの部分は、NDK/RDMA 機能を提供するネットワーク アダプターです。 このタイプのアダプターは、RDMA 対応の NIC (RNIC) とも呼ばれます。 ソフトウェアの部分は、NDKPI インターフェイスを実装する、NDK 対応ミニポート ドライバーです。

RDMA の Windows 実装には、ネットワーク ダイレクト (ND) が呼び出されます。 カーネルの部分は、ネットワーク ダイレクト カーネル (NDK) と呼ばれます。

NDK プロバイダーは、NDK 対応のミニポート アダプターに割り当てられた IPv4 と IPv6 の両方のアドレスを使用して直接ネットワーク接続をサポートする必要があります。

RDMA の詳細については、次を参照してください。 [RDMA でバック グラウンド読み込み](background-reading-on-rdma.md)します。

### <a name="the-ndk-provider"></a>NDK プロバイダー

NDK プロバイダーは、NDKPI インターフェイスを実装するミニポート ドライバーです。

NDK プロバイダーが読み込まれ、PnP マネージャーによって初期化されます。 詳細については、次を参照してください。 [NDK 対応のミニポート ドライバーの初期化](initializing-an-ndk-capable-miniport-driver.md)と[NDK ミニポート アダプターの初期化](initializing-an-ndk-miniport-adapter.md)します。

NDK プロバイダーがロードされ、初期化、NDK コンシューマーから要求を処理する準備ができてです。 プロバイダーの機能への呼び出しとしてこれらの要求が到着します。

NDK コンシューマーからの要求を処理するときに、プロバイダーがコンシューマーの NDK コールバック関数を呼び出すことができます。 これらを以下に説明[NDKPI コンシューマーのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

NDK プロバイダーが記載されている、NDKPI インターフェイスのすべての要素を実装する必要があります、 [NDKPI 参照](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)を除く、 [NDKPI コンシューマーのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

### <a name="the-ndk-consumer"></a>NDK コンシューマー

NDK コンシューマーは、SMB サーバーとクライアントなどのカーネル モードの Windows コンポーネントです。

**注**  このドキュメントでは、NDK コンシューマーを実装する方法については説明しません。 NDKPI コンシューマー デバイス ドライバー インターフェイス (DDI) は、独自の Windows の内部インターフェイスです。

 

NDK コンシューマーを呼び出して、プロバイダーの*NdkOpenAdapter* ([*オープン\_NDK\_アダプター\_ハンドラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler)) にコールバック関数アダプター オブジェクトを作成し、 *NdkCloseAdapter* ([*NDK\_FN\_閉じます\_オブジェクト*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_close_object)) を閉じます。 プロバイダーが、そのアダプタ オブジェクトを作成、コンシューマーは、追加の NDK オブジェクトを作成するその他のプロバイダーのコールバック関数を呼び出します。

NDK コンシューマーの実装、 [NDKPI コンシューマーのコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)、NDK プロバイダーによって呼び出されします。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






