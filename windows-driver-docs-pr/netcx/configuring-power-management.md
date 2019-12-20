---
title: 電源管理の構成
description: 電源管理の構成
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 電源管理の構成, NetCx 電源管理の構成
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: a3466dfa505558afebc4af2c207470df5d9e695b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210784"
---
# <a name="configuring-power-management"></a>電源管理の構成

このトピックでは、NetAdapterCx クライアントドライバーで電源管理機能を構成する方法について説明します。

クライアントドライバーは WDF ドライバーであるため、実装の多くは他の WDF ドライバーと同じですが、で追加できる NetAdapterCx 固有のオプションがいくつかあります。

一般的な WDF の動作の詳細については、次のページを参照してください。

*  クライアントは、「[関数ドライバーでの PnP と電源管理のサポート](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)」で説明されているように、電源遷移の通知を受信するためにオプションの WDF イベントコールバックを登録します。
*  WDF クライアントでの PnP および電源コールバック関数の登録の詳細については、「[関数ドライバーでのデバイスオブジェクトの作成](../wdf/creating-device-objects-in-a-function-driver.md)」を参照してください。
*  デバイスがシステム全体の低電力状態からシステムをウェイクアップする方法の詳細については、「[システムウェイクアップのサポート](../wdf/supporting-system-wake-up.md)」を参照してください。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>ネットワークアダプターの電源機能の設定

標準の WDF 電源管理機能を構成した後、次の手順では、ネットワークアダプターの電源機能を設定します。 電源機能は、低電力プロトコルオフロード機能と wake ソース機能という2つのカテゴリに分類されます。 クライアントドライバーは、ハードウェアに適した次の方法を呼び出すことによって、プロトコルオフロード機能を設定します。

- [**NetAdapterPowerOffloadSetArpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetarpcapabilities)
- [**NetAdapterPowerOffloadSetNSCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetnscapabilities)

次に、クライアントドライバーは、ハードウェアがサポートする wake on LAN (WoL) 機能を設定するために、次のいずれかの方法を呼び出します。

- [**NetAdapterWakeSetBitmapCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetbitmapcapabilities)
- [**NetAdapterWakeSetMagicPacketCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmagicpacketcapabilities)
- [**NetAdapterWakeSetMediaChangeCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmediachangecapabilities)
- [**NetAdapterWakeSetPacketFilterCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetpacketfiltercapabilities)

次の例では、クライアントドライバーが電力機能を初期化する方法を示しています。この動作は、net アダプターの開始中、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に行われます。 この例では、クライアントドライバーはビットマップ、メディアの変更、およびパケットフィルターのウェイクアップ機能を設定します。

```C++
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
// Set media change wake capabilties
//
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES mediaChangeCapabilities;
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES_INIT(&mediaChangeCapabilities);

mediaChangeCapabilities.MediaConnect = TRUE;
mediaChangeCapabilities.MediaDisconnect = TRUE;

NetAdapterWakeSetMediaChangeCapabilities(Adapter, &mediaChangeCapabilities);

//
// Set packet filter wake capabilties 
//
if(deviceContext->SelectiveSuspendSupported)
{
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES packetFilterCapabilities;
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES_INIT(&packetFilterCapabilities);
    
    packetFilterCapabilities.PacketFilterMatch = TRUE;

    NetAdapterWakeSetPacketFilterCapabilities(Adapter, &packetFilterCapabilities);
}
```

クライアントは[*EVT_NET_DEVICE_PREVIEW_POWER_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_power_offload)および[*EVT_NET_DEVICE_PREVIEW_WAKE_SOURCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_wake_source)コールバック関数を登録して、着信プロトコルオフロードとウェイクパターンを受け入れたり拒否したりできます。 これらの省略可能なコールバックのいずれかを登録する場合は、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に、net アダプターの開始時に行う必要があります。

## <a name="programming-protocol-offload-and-wake-patterns"></a>プロトコルオフロードとスリープ解除パターンのプログラミング

[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)と[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)のコールバック関数では、ドライバーは有効なウェイクパターンを反復処理し、プロトコルをオフロードしてハードウェアにプログラムします。

次の例では、クライアントドライバーが wake on マジックパケットエントリを確認するためにウェイクパターンリストを反復処理し、次に電源オフロードリストを反復処理して IPv4 ARP プロトコルオフロードを処理する方法を示します。

```C++
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