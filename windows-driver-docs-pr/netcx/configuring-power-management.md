---
title: 電源管理の構成
description: 電源管理の構成
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx NetCx 電源管理の構成、電源管理の構成
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: de18f627adbca92c95da655f01db06c5db76c29c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531271"
---
# <a name="configuring-power-management"></a>電源管理の構成

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアント ドライバーで電源管理機能を構成する方法について説明します。

クライアント ドライバーは WDF ドライバーであるため、WDF ドライバーと同じでは、多くの実装とはいくつかのオプションで追加できる NetAdapterCx に固有です。

詳細については、共通の WDF 動作は、次のページを参照してください。

*  」の説明に従って、クライアントは省略可能な電源の遷移の通知を受け取る WDF イベントのコールバックを登録します。 [PnP をサポートしていると関数のドライバーでの電源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)します。
*  WDF のクライアントでの PnP と電力のコールバック関数の登録方法の詳細については、次を参照してください。 [Function ドライバーのデバイス オブジェクトの作成](../wdf/creating-device-objects-in-a-function-driver.md)です。
*  デバイスがシステム全体の低電力状態からシステムをスリープ解除する方法の詳細については、「[システムのウェイク アップをサポートしている](../wdf/supporting-system-wake-up.md)します。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>ネットワーク アダプターの設定の 電源機能

標準の WDF 電源管理機能を構成した後、次の手順を呼び出す[ **NetAdapterSetPowerCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetpowercapabilities)電源、ネットワーク アダプターの機能を設定します。

次の例は、初期化、および、ネット アダプターを開始するときに、呼び出す前に、クライアントが通常は NETPOWERSETTINGS オブジェクトを構成する方法を示しています[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart):。

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

クライアントを登録できます[ *EVT_NET_ADAPTER_PREVIEW_PROTOCOL_OFFLOAD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_preview_protocol_offload)と[ *EVT_NET_ADAPTER_PREVIEW_WAKE_PATTERN* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_preview_wake_pattern)着信のプロトコルを承認または拒否のコールバック関数では、オフロードし、復帰のパターン。 これらの省略可能なコールバックのいずれかを登録する場合は、する必要がありますこれを行う呼び出しの前に、ネット アダプターの開始中に[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)します。

## <a name="programming-protocol-offload-and-wake-patterns"></a>プログラミングのプロトコルがオフロードし、復帰のパターン

その[ *EvtDeviceArmWakeFromS0* ](https://msdn.microsoft.com/library/windows/hardware/ff540843)と[ *EvtDeviceArmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)コールバック関数では、ドライバーは、有効を反復処理ウェイク アップのパターンとプロトコルは、負荷を軽減し、ハードウェアへのプログラムします。

最初に呼び出すことによって、アダプターに関連付けられている NETPOWERSETTINGS オブジェクトへのハンドルを取得[ **NetAdapterGetPowerSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptergetpowersettings)から[ *EvtDeviceArmWakeFromS0* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)または関連するコールバック関数。  次の例では、ウェイク アップのパターンを反復処理する方法を示します。

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

同じプロトコルを反復処理するメカニズムがオフロードを使用して、クライアントで[ **NetPowerSettingsGetProtocolOffloadCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffloadcount)、 [ **NetPowerSettingsGetProtocolOffload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffload)と[ **NetPowerSettingsIsProtocolOffloadEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsisprotocoloffloadenabled)します。
