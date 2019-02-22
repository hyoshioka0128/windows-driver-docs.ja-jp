---
title: NetAdapterCx オブジェクトの概要
description: NetAdapterCx オブジェクトの概要
ms.assetid: 1635C737-42C6-4957-A3E0-1184A5545441
keywords:
- オブジェクトの概要を NetCx NetAdapterCx のオブジェクトの概要
ms.date: 08/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: fadb848c2f720c5afca7f011f7dffabf70aca3a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551625"
---
# <a name="summary-of-netadaptercx-objects"></a>NetAdapterCx オブジェクトの概要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図は、NetAdapterCx オブジェクトの既定のプロセスの親子関係を示します。 親オブジェクトが、図の上部にあるが、WDFDEVICE オブジェクトの子をそのため、たとえばし、NETADAPTER オブジェクトが既定です。 二重のボックスでは、複数のインスタンスを持つオブジェクトが示されます。

![NetAdapterCx の概要が NetAdapterCx クライアント ドライバー オブジェクト](images/netcx-adapter-object-model.png "NetAdapterCx クライアント ドライバーの概要の NetAdapterCx オブジェクト")

WDFDEVICE オブジェクトは、標準[フレームワーク オブジェクト](../wdf/wdf-objects.md)デバイスを表します。 NETADAPTER オブジェクトは、すべてのネットワーク I/O のエンドポイントは、ネットワーク インターフェイスを表します。 WDFDEVICE を各 NETADAPTER の親オブジェクトの中で、WDFDEVICE ごとの複数の NETADAPTER オブジェクトがあることができます。

プライマリ NETADAPTER と呼ばれる、*既定のアダプター*します。 ほとんどのネットワーク インターフェイス カード (NIC) ドライバーでは、物理デバイスの 1 つの NETADAPTER のみがあるが、複数のスロットは、サーバーの NIC を管理する場合、クライアント ドライバーによっては 1 つ以上の NETADAPTER にあります。 別の例として[モバイル ブロード バンド WDF クラス拡張 (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)クライアント ドライバーが追加のパケット データ プロトコル (PDP) コンテキストを表す 1 つ以上の NETADAPTER オブジェクトを管理します。 

> [!TIP]
> 現時点では、既定のアダプターは、1 つのユーザー モード アプリケーションに表示されるだけです。

既定のアダプターは初期化され、クライアント ドライバーの内から作成する必要があります[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add
)コールバック関数を呼び出して[ **NetDefaultAdapterInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netdefaultadapterinitallocate)と[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)します。 次に、その必要があります内から開始するドライバーの[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を呼び出して[ **NetAdapterStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). 呼び出しの前に**NetAdapterStart**ドライバーのリンク層の機能、電源機能、データパス機能など、アダプターの機能の設定、スケーリングが表示されることができます必要に応じて機能、およびハードウェア オフロード機能。

中に、必要に応じて複数の NETADAPTER オブジェクトを追加できる*EvtDeviceAdd*します。 既定値で初期化が 1 つだけでなく新しい各 NETADAPTER [ **NetAdapterInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterinitallocate)の代わりに**NetDefaultAdapterInitAllocate**します。 それ以外の場合、それらを作成する手順は同じですと同様に、後でセッションが開始されます*EvtDevicePrepareHardware*します。

間のリレーションシップの詳細については[ **NET_RING_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)、 [ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)、および[ **NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)を参照してください[パケット記述子と拡張機能](packet-descriptors-and-extensions.md#storage-of-packet-descriptors)します。
