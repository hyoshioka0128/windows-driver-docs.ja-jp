---
title: NetAdapterCx ハードウェアのオフロード
description: NetAdapterCx のオフロード
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF ネットワークアダプタークラス拡張のオフロード、NetAdapterCx ハードウェアのオフロード、NetAdapterCx のオフロード、NetAdapter のオフロード
ms.date: 01/18/2019
ms.custom: 19H1
ms.openlocfilehash: c84c858e33a3b7affaa5ce416b19688ddfc603aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838277"
---
# <a name="netadaptercx-hardware-offloads"></a>NetAdapterCx ハードウェアのオフロード

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

Windows TCP/IP スタックでは、パフォーマンスを向上させるために、適切なタスクオフロード機能を備えたネットワークインターフェイスカード (NIC) にタスクをオフロードすることができます。

## <a name="overview-of-offloads-in-netadaptercx"></a>NetAdapterCx のオフロードの概要

NetAdapterCx は、オフロードの構成とオフロード機能の管理に重点を置いています。 クライアントドライバーは、ハードウェアオフロード機能の単純な構成を指定するだけで、機能の変更を通知するためのコールバックを登録する必要があります。 

このガイドでは、NetAdapterCx でのハードウェアオフロードの主要概念の概要について説明します。

- ハードウェアオフロード機能は、初期化時にネットワークアダプターのハードウェアによって提供され、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前にアドバタイズする必要があります。
- ドライバーは、標準のレジストリキーワードのチェックを気にする必要はありません。 NetAdapterCx は、アクティブなオフロード機能を有効にするときに、レジストリキーワードを確認し、それらを優先します。
- ネットワークアダプターの*アクティブな*オフロード機能は、ネットワークアダプターが現在実行するようにプログラミングされている機能です。 これらは、以前にクライアントドライバーによってアドバタイズされたハードウェア機能のサブセットです。
- TCP/IP スタックまたはそれ以降のプロトコルドライバーは、ネットワークアダプターのアクティブな機能の変更を要求できます。 クライアントドライバーは、アクティブなオフロード機能の変更を通知するために、コールバックを NetAdapterCx に登録します。
- オフロードにパケット拡張が必要な場合は、ネットワークアダプターがハードウェアオフロードのサポートをアドバタイズするときに自動的に登録されます。

クライアントドライバーは、最小限の機能セットを NetAdapterCx にアドバタイズします。 これらには、クライアントドライバーでサポートされているすべてのオフロードの組み合わせに関する詳細な機能の詳細は含まれません。 たとえば、IPOptions、IPExtensions、TCPOptions のいずれがサポートされているかなどです。つまり、クライアントドライバーは、提供された機能のすべての組み合わせに対してオフロードを実行します。 たとえば、IPv4 のサポートは IPOptions のサポートを意味し、IPv6 のサポートは IPExtensions のサポートを意味し、TCP のサポートは TCPOptions のサポートを意味します。 

ハードウェアが特定の組み合わせを処理できない場合は、その機能のサポートを宣言しないか、このようなパケットが発生したときにソフトウェアフォールバックを実行する必要があります。

次のオフロードは、NetAdapterCx と Windows TCP/IP スタックでサポートされています。

| オフロード名 | 説明 |
| --- | --- |
| Checksum | IP および TCP チェックサムの計算と検証を、NIC にオフロードします。 |
| Large send offload (LSO) | IPv4 および IPv6 用の大きな TCP パケットのセグメント化をオフロードする。 |

## <a name="configuring-hardware-offloads"></a>ハードウェアのオフロードの構成

クライアントドライバーは、最初に、ネットアダプターの初期化中にハードウェアのチェックサムオフロード機能を提供します。 これは、ネットワークアダプターを起動するときに、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)のコンテキスト内で発生する可能性があります。 開始するために、クライアントドライバーはサポートされているオフロードごとに機能構造を割り当て、それらを初期化して、適切な**NetAdapterOffloadSetXxxCapabilities**メソッドを呼び出してそれらを NetAdapterCx に登録します。 **NET_ADAPTER_OFFLOAD_XxX_CAPABILITIES_INIT**の呼び出し中に、ドライバーはコールバック関数へのポインターを提供します。これは、アクティブなハードウェアオフロード機能が変更された場合に、システムによって後で呼び出されます。

この例は、クライアントドライバーがハードウェアオフロード機能を設定する方法を示しています。

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
                                                   TRUE,    // UDP
                                                   MyEvtAdapterOffloadSetChecksum);

    // Set the current checksum offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetChecksumCapabilities(NetAdapter,
                                             &checksumOffloadCapabilities);

    // Configure the hardware's LSO offload capabilities
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES lsoOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT(&lsoOffloadCapabilities,
                                              TRUE,         // IPv4
                                              TRUE,         // IPv6
                                              MY_LSO_OFFLOAD_SIZE_MAX,
                                              MY_LSO_OFFLOAD_MIN_SEGMENT_COUNT,
                                              MyEvtAdapterOffloadSetLso);

    // Set the current LSO offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetLsoCapabilities(NetAdapter,
                                        &lsoOffloadCapabilities);   
}
```

## <a name="updating-hardware-offloads"></a>ハードウェアのオフロードを更新しています

TCP/IP スタックまたはそれ以降のプロトコルドライバーがネットワークアダプターのアクティブな機能の変更を要求した場合、NetAdapterCx は、以前に登録されたクライアントドライバーの*EVT_NET_ADAPTER_OFFLOAD_SET_XxX*コールバック関数を呼び出します。アダプターの初期化。 この関数では、システムは NETOFFLOAD obbject で更新された機能を提供します。この機能は、クライアントドライバーがクエリを実行してオフロード機能を更新するために使用できます。

次の例は、クライアントドライバーがチェックサムオフロード機能を更新する方法を示しています。

```C++
VOID
MyEvtAdapterOffloadSetChecksum(
    NETADAPTER  NetAdapter,
    NETOFFLOAD  Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->HardwareIpChecksum = NetOffloadIsChecksumIPv4Enabled(Offload);
    adapterContext->HardwareTcpChecksum = NetOffloadIsChecksumTcpEnabled(Offload);
    adapterContext->HardwareUdpChecksum = NetOffloadIsChecksumUdpEnabled(Offload);

    // Update the new hardware checksum offload capabilities
    MyUpdateHardwareChecksum(adapterContext);
}
```

次の類似の例では、クライアントドライバーが LSO のオフロード機能を更新する方法を示しています。

```C++
VOID
MyEvtAdapterOffloadSetLso(
    NETADAPTER NetAdapter,
    NETOFFLOAD Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->LSOv4 = NetOffloadIsLsoIPv4Enabled(Offload) ? 
        LsoOffloadEnabled : LsoOffloadDisabled;
    adapterContext->LSOv6 = NetOffloadIsLsoIPv6Enabled(Offload) ?
        LsoOffloadEnabled : LsoOffloadDisabled;

    // Enable hardware checksum if LSO is enabled
    MyUpdateHardwareChecksum(adapterContext);
}
```

## <a name="related-links"></a>関連リンク

[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_offload_checksum_capabilities)

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_offload_checksum_capabilities_init)

[**NetAdapterOffloadSetChecksumCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapteroffloadsetchecksumcapabilities)

[*EvtNetAdapterOffloadSetChecksum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_offload_set_checksum)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_lso_capabilities)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_lso_capabilities_init)

[**NetAdapterOffloadSetLsoCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetlsocapabilities)

[*EvtNetAdapterOffloadSetLso*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_lso)
