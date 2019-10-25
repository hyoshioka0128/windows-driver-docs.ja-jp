---
title: 電源管理の構成
description: 電源管理の構成
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 電源管理の構成, NetCx 電源管理の構成
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17468822a966aafe4e6cdf5dd79f149e9dfe87c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835532"
---
# <a name="configuring-power-management"></a>電源管理の構成

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアントドライバーで電源管理機能を構成する方法について説明します。

クライアントドライバーは WDF ドライバーであるため、実装の多くは他の WDF ドライバーと同じですが、で追加できる NetAdapterCx 固有のオプションがいくつかあります。

一般的な WDF の動作の詳細については、次のページを参照してください。

*  クライアントは、「[関数ドライバーでの PnP と電源管理のサポート](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)」で説明されているように、電源遷移の通知を受信するためにオプションの WDF イベントコールバックを登録します。
*  WDF クライアントでの PnP および電源コールバック関数の登録の詳細については、「[関数ドライバーでのデバイスオブジェクトの作成](../wdf/creating-device-objects-in-a-function-driver.md)」を参照してください。
*  デバイスがシステム全体の低電力状態からシステムをウェイクアップする方法の詳細については、「[システムウェイクアップのサポート](../wdf/supporting-system-wake-up.md)」を参照してください。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>ネットワークアダプターの電源機能の設定

標準の WDF 電源管理機能を構成した後、次の手順では、 [**NetAdapterSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetpowercapabilities)を呼び出してネットワークアダプターの電源機能を設定します。

次の例は、NETPOWERSETTINGS オブジェクトを初期化して構成する方法を示しています。このオブジェクトは、通常、クライアントが net アダプターを起動するときに、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に実行します。

```C++
NET_ADAPTER_POWER_CAPABILITIES     powerCaps;
NET_ADAPTER_POWER_CAPABILITIES_INIT(&powerCaps);

powerCaps.Flags = NET_ADAPTER_POWER_WAKE_PACKET_INDICATION;

powerCaps.SupportedMediaSpecificWakeUpEvents = NET_ADAPTER_WLAN_WAKE_ON_AP_ASSOCIATION_LOST;
powerCaps.SupportedProtocolOffloads = NET_ADAPTER_PROTOCOL_OFFLOAD_ARP | NET_ADAPTER_PROTOCOL_OFFLOAD_NS;
powerCaps.SupportedWakePatterns = NET_ADAPTER_WAKE_BITMAP_PATTERN;
powerCaps.SupportedWakeUpEvents = NET_ADAPTER_WAKE_ON_MEDIA_CONNECT | NET_ADAPTER_WAKE_ON_MEDIA_DISCONNECT;

powerCaps.EvtAdapterPreviewWakePattern = EvtAdapterPreviewWakePattern;
powerCaps.EvtAdapterPreviewProtocolOffload = EvtAdapterPreviewProtocolOffload;

NetAdapterSetPowerCapabilities(NetAdapter, &powerCaps);
```

クライアントは、 [*EVT_NET_ADAPTER_PREVIEW_PROTOCOL_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_preview_protocol_offload)および[*EVT_NET_ADAPTER_PREVIEW_WAKE_PATTERN*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_preview_wake_pattern)コールバック関数を登録して、受信プロトコルオフロードとウェイクパターンを受け入れたり拒否したりできます。 これらの省略可能なコールバックのいずれかを登録する場合は、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に、net アダプターの開始時に行う必要があります。

## <a name="programming-protocol-offload-and-wake-patterns"></a>プロトコルオフロードとスリープ解除パターンのプログラミング

[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)と[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)のコールバック関数では、ドライバーは有効なウェイクパターンを反復処理し、プロトコルをオフロードしてハードウェアにプログラムします。

まず、 [*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)または関連するコールバック関数から[**NetAdapterGetPowerSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptergetpowersettings)を呼び出すことによって、アダプターに関連付けられている netpowersettings オブジェクトへのハンドルを取得します。  次の例は、スリープ解除パターンを反復処理する方法を示しています。

```C++
NTSTATUS
EvtDeviceArmWakeFromS0(
    WDFDEVICE     Device
)
{

    NETADAPTER adapter = GetDeviceContext(Device)->Adapter;
    NETPOWERSETTINGS powerSettings = NetAdapterGetPowerSettings(adapter);

    ULONG wakeUpFlags = NetPowerSettingsGetEnabledWakeUpFlags(powerSettings);
     
    if (wakeUpFlags & NET_ADAPTER_WAKE_ON_MEDIA_DISCONNNECT)
    {
        // ...
    }

    // Iterate through stored wake patterns and query which ones
    // are enabled and should be programmed to hardware

    for (ULONG i = 0; i < NetPowerSettingsGetWakePatternCount(powerSettings); i++)
    {
        PNDIS_PM_WOL_PATTERN wakePattern = NetPowerSettingsGetWakePattern(powerSettings, i);

        if (NetPowerSettingsIsWakePatternEnabled(powerSettings, wakePattern))
        {
            // ...
        }

    }

    return STATUS_SUCCESS;
}
```

クライアントは、 [**NetPowerSettingsGetProtocolOffloadCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffloadcount)、 [**NetPowerSettingsGetProtocolOffload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffload) 、および[**NetPowerSettingsIsProtocolOffloadEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsisprotocoloffloadenabled)を使用して、プロトコルのオフロードを反復処理するのと同じメカニズムを使用します。
