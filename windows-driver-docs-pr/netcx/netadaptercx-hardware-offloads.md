---
title: NetAdapterCx ハードウェア オフロード
description: NetAdapterCx オフロード
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF ネットワーク アダプター クラスの拡張機能は、オフロード、NetAdapterCx ハードウェア オフロード、NetAdapterCx オフロード、NetAdapter の負荷を軽減
ms.date: 07/31/2018
ms.openlocfilehash: 75e01c0c7639b7c5ea5e81aa29ec9f45782649f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572376"
---
# <a name="netadaptercx-hardware-offloads"></a>NetAdapterCx ハードウェア オフロード

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

そのパフォーマンスを向上させる Windows TCP/IP スタックは適切なタスク オフロード機能を含むネットワーク インターフェイス カード (NIC) にいくつかのタスクをオフロードできます。

## <a name="overview-of-offloads-in-netadaptercx"></a>NetAdapterCx でオフロードの概要

NetAdapterCx は、簡単なオフロードの構成と管理のオフロード機能について説明します。 のみ、クライアント ドライバーは、ハードウェアのオフロード機能の簡単な構成を指定し、機能の変更の通知コールバックを登録する必要があります。 

このガイドでは、負荷を軽減 NetAdapterCx でハードウェアの主要な概念の概要を提供します。

- ハードウェア オフロード機能の初期化中にネットワーク アダプターのハードウェアによって提供および呼び出す前に提供する必要があります[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)します。
- ドライバー確認標準レジストリ キーワードについて心配する必要はありません。 NetAdapterCx はレジストリ キーワードをチェックし、オフロード機能をアクティブなを有効にするには、します。
- *Active*ネットワーク アダプターは、現在のネットワーク アダプターのオフロード機能を実行するようにプログラミングできます。 これらは、以前のクライアント ドライバーによってアドバタイズされたハードウェア機能のサブセットです。
- TCP/IP スタックまたは上位のプロトコル ドライバーには、ネットワーク アダプターのアクティブな機能の変更を要求できます。 クライアント ドライバーでは、アクティブなオフロード機能の変更の通知を受ける NetAdapterCx コールバックを登録します。
- パケットの拡張機能は、オフロードの必要がある場合、ネットワーク アダプター ハードウェア オフロード用のサポートをアドバタイズするときに自動的に登録されます。

クライアント ドライバーでは、NetAdapterCx 機能の最小セットを提供します。 これらのクライアント ドライバーでサポートされているすべてのオフロードの組み合わせの詳細な機能の詳細は含まれません。 たとえば、これは、IPOptions、IPExtensions または tcpoptions ですがサポートされているかどうかなど。つまり、クライアント ドライバーは、提供された機能のすべての組み合わせで、オフロードを実行する責任を負います。 IPv4 意味 IPOptions のサポートのサポートなど IPExtensions のサポートを意味する IPv6 のサポート、および TCP tcpoptions ですのサポートを意味するをサポートします。 

ハードウェアが特定の組み合わせを処理できない場合にする必要があります機能のサポートを宣言かこのようなパケットを見つけたときに、ソフトウェア フォールバックを実行します。

NetAdapterCx して、Windows TCP/IP スタックは、次のオフロードがサポートされています。

| 名前をオフロードします。 | 説明 |
| --- | --- |
| チェックサム | 計算と NIC に ip アドレスと TCP チェックサムの検証をオフロードします。 |
| 大量送信オフロード (LSO) | IPv4 と IPv6 の大きな TCP パケットのセグメント化をオフロードします。 |

## <a name="example"></a>例

まず、クライアント ドライバーは、ネット アダプターの初期化中に、ハードウェアのチェックサム オフロード機能を提供します。 コンテキスト内で発生する可能性がありますこれ[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)ネット アダプターを起動する場合。 最初に、クライアント ドライバー サポートされている各オフロード用の機能の構造を割り当てに、変数を初期化し、適切な**NetAdapterOffloadSetXxxCapabilities** NetAdapterCx に登録するメソッド。 呼び出し中に**NetAdapterOffloadSetXxxCapabilities**ドライバーがアクティブなハードウェア オフロード機能変更する場合に、システムが後で呼び出されるコールバック関数へのポインターを提供します。

この例では、クライアント ドライバーがそのハードウェア オフロード機能を設定する方法を示します。

```C++
VOID
MyAdapterSetOffloadCapabilities(
    NETADAPTER NetAdapter
)
{
    // Configure the hardware's checksum offload capabilities
    NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES checksumOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES_INIT(&checksumOffloadCapabilities,
                                                   TRUE,    // IPv4
                                                   TRUE,    // TCP
                                                   TRUE);   // UDP

    // Set the current checksum offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetChecksumCapabilities(NetAdapter,
                                             &checksumOffloadCapabilities,
                                             MyEvtAdapterOffloadSetChecksum);

    // Configure the hardware's LSO offload capabilities
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES lsoOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT(&lsoOffloadCapabilities,
                                              TRUE,         // IPv4
                                              TRUE,         // IPv6
                                              MY_LSO_OFFLOAD_SIZE_MAX,
                                              MY_LSO_OFFLOAD_MIN_SEGMENT_COUNT);

    // Set the current LSO offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetLsoCapabilities(NetAdapter,
                                        &lsoOffloadCapabilities,
                                        MyEvtAdapterOffloadSetLso);   
}
```

## <a name="related-links"></a>関連リンク

[Packet descriptors and extensions (パケットの記述子と拡張機能)](packet-descriptors-and-extensions.md)
