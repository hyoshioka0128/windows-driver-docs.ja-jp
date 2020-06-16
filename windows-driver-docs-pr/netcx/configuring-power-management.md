---
title: NetAdapterCx 電源管理の構成
description: 電源管理の構成
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 電源管理の構成, NetCx 電源管理の構成
ms.date: 06/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 39ae39450599b557f73c52eebe19ee64b1ce3e97
ms.sourcegitcommit: 7cc3143fc4b7c88dbebb4bdaeff666d290aa1a16
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84780690"
---
# <a name="configuring-netadaptercx-power-management"></a>NetAdapterCx 電源管理の構成

すべての NetAdapterCx クライアントドライバーは、すべての WDF ドライバーと同様の電源管理機能を備えた Windows Driver Framework (WDF) ドライバーです。 NetAdapterCx ドライバーには、この記事で詳しく説明されているように、ネットワーク固有の追加の電源構成が必要です。

一般的なネットワークデバイスでは、3つの一般的な電源管理機能がサポートされています。

- ネットワークデバイスは、OS によって指示されたときに、低電力 (Dx) 状態になることがあります。
  - クライアントドライバーは、オプションの WDF イベントコールバックを登録して、電源遷移の通知を受信します。詳細については、「[関数ドライバーでの PnP および電源管理のサポート](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)」を参照してください。

  - システムが動作中 (S0) 状態になっている間にネットワークデバイスがその Dx 状態に入ると、クライアントドライバーはアイドル状態の電源をサポートする必要があります。 「[アイドル状態の電源ダウンをサポート](../wdf/supporting-idle-power-down.md)する」を参照してください。

- ネットワークデバイスが Dx 状態にある場合は、事前に構成されたウェイク状態が発生したときにウェイクアップ信号をトリガーできます。
  - WDF デバイスがシステム全体の低電力状態からシステムをウェイクアップする方法の詳細については、「[システムウェイクアップをサポート](../wdf/supporting-system-wake-up.md)する」を参照してください。

  - NetAdapterCx は、ハードウェアがどのネットワークイベントに対して wake サポートを提供しているかを宣言するために、クライアントドライバー用の Api を提供します。 後述の「[ネットワークアダプターの電源機能の設定](#setting-power-capabilities-of-the-network-adapter)」を参照してください。

- ネットワークデバイスが Dx 状態にある場合でも、一般的に使用されるいくつかのネットワーク要求に応答して、ホストシステムの起動を行わずに、ネットワーク上でホストシステムの存在を維持することができます。 後述の「[ネットワークアダプターの電源機能の設定](#setting-power-capabilities-of-the-network-adapter)」を参照してください。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>ネットワークアダプターの電源機能の設定

WDF の電源管理機能を構成したら、次の手順として、ネットワークアダプターの電源機能を設定します。 電源機能は、[低電力プロトコルオフロード機能](#low-power-protocol-offload-capabilities)と[ウェイクアップ機能](#wake-up-capabilities)という2つのカテゴリに分類されます。

### <a name="low-power-protocol-offload-capabilities"></a>低電力プロトコルオフロード機能

Windows ネットワークスタックでこの機能を使用する方法の背景情報については、「 [NDIS 電源管理のプロトコルオフロード](../network/protocol-offloads-for-ndis-power-management.md)」を参照してください。

クライアントドライバーは、ハードウェアに適した次の方法を呼び出すことによって、低電力プロトコルオフロード機能を設定します。

- [**NetAdapterPowerOffloadSetArpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetarpcapabilities)
- [**NetAdapterPowerOffloadSetNSCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetnscapabilities)

### <a name="wake-up-capabilities"></a>ウェイクアップ機能

クライアントドライバーは、次のいずれかの方法で、デバイスが低電力状態 (Dx) のときにハードウェアがサポートするウェイク機能を設定します。

- [**NetAdapterWakeSetBitmapCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetbitmapcapabilities)
- [**NetAdapterWakeSetMagicPacketCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmagicpacketcapabilities)
- [**NetAdapterWakeSetMediaChangeCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmediachangecapabilities)
- [**NetAdapterWakeSetPacketFilterCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetpacketfiltercapabilities)

### <a name="power-consumption-and-resume-latency"></a>電力消費と再開待機時間

ネットワークデバイスが Dx にある場合、オフロードと arm 用の arm の実行に電力を消費します。 デバイスが Dx からウェイクアップを開始した後は、デバイスがパケットを再び転送できるようになるまでに遅延が発生します。 デバイスが Dx の間に消費する電力が少なくなると同時に、再開の待機時間が長くなります。

次の表は、各ウェイクアップ機能の電力消費と再開待機時間のトレードオフに関する一般的なガイドラインを示しています。

> [!IMPORTANT]
> 一部の情報は prereleased 製品に関連していますが、商業リリースの前に大幅に変更される可能性があります。 マイクロソフトは、提供された情報に関して明示的または黙示的に一切の保証を行いません。 特定のデバイスの種類の詳細については、メディア固有のドキュメントおよび[Windows ハードウェア互換性プログラム (WHCP)](https://docs.microsoft.com/windows-hardware/design/compatibility/)を参照してください。
  
| ウェイク機能 | ウェイクイベント | 電力消費 | 再開待機時間
|-|-|-|-|
| PacketFilter | 構成された ReceivePacketFilter に一致するパケット | は、D0 の場合よりも小さくする必要があり、再開の待機時間が非常に短いように、デバイスを適切な状態に保つ必要があります。  | <= 10 ミリ秒
| Bitmap |構成済みビットマップパターンに一致するパケット | 再開待機時間にはより多くの緯度があるため、PacketFilter に設定されている場合よりも小さくなければなりません | <= 300 ミリ秒
| MagicPacket | マジックパケット | ビットマップに似ています。 | <= 300 ミリ秒
| MediaChange 場合 | 接続または切断されたメディア | ビットマップに似ています。 | <= 300 ミリ秒

次の例は、クライアントドライバーがその電源機能を初期化する方法を示しています。 これは、net アダプターの開始時に、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に行います。 この例では、クライアントドライバーはビットマップ、メディアの変更、およびパケットフィルターのウェイクアップ機能を設定します。

```cpp
//
// Set bitmap wake capabilities
//
NET_ADAPTER_WAKE_BITMAP_CAPABILITIES bitmapCapabilities;
NET_ADAPTER_WAKE_BITMAP_CAPABILITIES_INIT(&bitmapCapabilities);

bitmapCapabilities.BitmapPattern = TRUE;
bitmapCapabilities.MaximumPatternCount = deviceContext->PowerFiltersSupported;
bitmapCapabilities.MaximumPatternSize = 256;

NetAdapterWakeSetBitmapCapabilities(Adapter, &bitmapCapabilities);

//
// Set media change wake capabilities
//
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES mediaChangeCapabilities;
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES_INIT(&mediaChangeCapabilities);

mediaChangeCapabilities.MediaConnect = TRUE;
mediaChangeCapabilities.MediaDisconnect = TRUE;

NetAdapterWakeSetMediaChangeCapabilities(Adapter, &mediaChangeCapabilities);

//
// Set packet filter wake capabilities
//
if(deviceContext->SelectiveSuspendSupported)
{
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES packetFilterCapabilities;
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES_INIT(&packetFilterCapabilities);

    packetFilterCapabilities.PacketFilterMatch = TRUE;

    NetAdapterWakeSetPacketFilterCapabilities(Adapter, &packetFilterCapabilities);
}
```

クライアントは、必要に応じて[*EVT_NET_DEVICE_PREVIEW_POWER_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_power_offload)を登録したり、コールバック関数を[*EVT_NET_DEVICE_PREVIEW_WAKE_SOURCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_wake_source)して、着信プロトコルオフロードとウェイクパターンを受け入れたり拒否したりすることができます。

## <a name="programming-protocol-power-offload-and-wake-patterns"></a>プロトコルの電源オフロードとスリープ解除パターンのプログラミング

デバイスの[電源](../wdf/power-down-and-removal-sequence-for-a-function-or-filter-driver.md)をオフにすると、ドライバーは、有効になっているウェイクパターンとプロトコル電力のオフロードを反復処理してハードウェアにプログラムします。 ドライバーは、 [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)および[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)コールバック関数でこれを行います。

次の例では、クライアントドライバーが wake on マジックパケットエントリを確認するためにウェイクパターンリストを反復処理し、次に電源オフロードリストを反復処理して IPv4 ARP プロトコルオフロードを処理する方法を示します。

```cpp
NTSTATUS
EvtDeviceArmWakeFromSx(
    WDFDEVICE     Device
)
{
    NETADAPTER adapter = GetDeviceContext(Device)->Adapter;

    //
    // Process wake source list
    //
    NET_WAKE_SOURCE_LIST wakeSourceList;
    NET_WAKE_SOURCE_LIST_INIT(&wakeSourceList);

    NetDeviceGetWakeSourceList(Device, &wakeSourceList);

    for(UINT32 i = 0; i < NetWakeSourceListGetCount(&wakeSourceList; i++); i++)
    {
        NETWAKESOURCE wakeSource = NetWakeSourceListGetElement(&wakeSourceList, i);
        NET_WAKE_SOURCE_TYPE const wakeSourceType = NetWakeSourceGetType(wakeSource);

        if(wakeSourceType == NetWakeSourceTypeMagicPacket)
        {
            // Enable magic packet wake for the adapter
            ..
            //
        }
    }

    //
    // Process power offload list
    //
    NET_POWER_OFFLOAD_LIST powerOffloadList;
    NET_POWER_OFFLOAD_LIST_INIT(&powerOffloadList);

    NetDeviceGetPowerOffloadList(Device, &powerOffloadList);

    for(UINT32 i = 0; i < NetPowerOffloadListGetCount(&powerOffloadList); i++)
    {
        NETPOWEROFFLOAD powerOffload = NetPowerOffloadGetElement(&powerOffloadList, i);
        NET_POWER_OFFLOAD_TYPE const powerOffloadType = NetPowerOffloadGetType(powerOffload);

        if(powerOffloadType == NetPowerOffloadTypeArp)
        {
            // Enable ARP protocol offload for the adapter
            ..
            //
        }
    }

    return STATUS_SUCCESS;
}
```

[高電力に戻るため](../wdf/power-up-sequence-for-a-function-or-filter-driver.md)に、ドライバーは通常、対応する[*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)および[*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)コールバックで、以前にプログラミングされたプロトコルの電力オフロードとウェイクパターンを無効にします。

## <a name="power-management-scenarios-for-modern-standby-system"></a>最新のスタンバイシステムの電源管理のシナリオ

> [!IMPORTANT]
> 最新のスタンバイプラットフォームの場合、ネットワークデバイスドライバーは次のことを行う必要があります。
>
> - [**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)を呼び出して、電源コールバックを登録します。
> - [**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)を呼び出して、システムが動作 (S0) 状態にあるときにデバイスアイドル状態をサポートします。
> - [**Wdfdeviceinitsetpowerpolicyeventcallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)を呼び出して、ウェイクアップコールバックを登録します。
> - デバイスの種類に適した[低電力プロトコルオフロード機能](#low-power-protocol-offload-capabilities)をサポートします。
> - デバイスの種類に適した[ウェイクアップ機能](#wake-up-capabilities)をサポートします。
>
> デバイスの種類の最新のスタンバイ要件については、メディア固有のドキュメントと WHCP をご覧ください。

OS は、ネットワークデバイスの電源ポリシーの決定に責任を持ちます。 たとえば、OS は、デバイスが Dx にアクセスする必要があるタイミングと、デバイスのスリープ解除が必要なネットワークイベントの種類を制御します。 デバイスドライバーの責任は、OS によって要求されたときに電力切り替えシーケンスを確実に実行し、OS によって設定されたウェイク状態のハードウェアを正しくプログラムすることです。

OS は、システム全体の電源ポリシーやユーザーの選択など、さまざまな要因に基づいて、電源ポリシーの決定を行います。 次に、最新のスタンバイシステムのネットワークデバイスで使用される一般的な電源ポリシーをいくつか示します。

> [!IMPORTANT]
> これらの電源ポリシーは OS の更新プログラムで変更される可能性があり、以下の情報が例として提供されています。 OS の特定のエンドツーエンド動作に対する依存関係は避ける必要があります。

- PC の画面がオンになっていて、ネットワークデバイスがアイドル状態されている場合、OS はデバイスに Dx にアクセスするように要求し、PacketFilter と MediaChange wake 用にデバイスを接続します。

- PC が最新のスタンバイ状態に入り、ネットワークデバイスがアイドル状態されると、OS は NIC に Dx にアクセスして、ビットマップ、MediaChange、マジックパケットウェイク用に接続するように指示します。

- PC が休止状態になると、OS は、NIC に対して Dx にアクセスし、マジックパケットスリープ解除するように指示します。
