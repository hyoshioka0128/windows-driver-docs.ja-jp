---
title: NetAdapterCx オブジェクトの概要
description: NetAdapterCx オブジェクトの概要
ms.assetid: 1635C737-42C6-4957-A3E0-1184A5545441
keywords:
- オブジェクトの概要を NetCx NetAdapterCx のオブジェクトの概要
ms.date: 11/01/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6e8a937b1e79ced499f0263d29977c611bd2cc1c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903304"
---
# <a name="summary-of-netadaptercx-objects"></a>NetAdapterCx オブジェクトの概要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図は、NetAdapterCx オブジェクトの既定のプロセスの親子関係を示します。 親オブジェクトは、図の上部にあるため、NETADAPTER の例のオブジェクトが、既定では、WDFDEVICE オブジェクトの子。 二重のボックスでは、複数のインスタンスを持つオブジェクトが示されます。

![NetAdapterCx の概要が NetAdapterCx クライアント ドライバー オブジェクト](images/netcx-adapter-object-model.png "NetAdapterCx クライアント ドライバーの概要の NetAdapterCx オブジェクト")

WDFDEVICE オブジェクトは、標準[フレームワーク オブジェクト](../wdf/wdf-objects.md)デバイスを表します。 NETADAPTER オブジェクトは、すべてのネットワーク I/O のエンドポイントは、ネットワーク インターフェイスを表します。 WDFDEVICE を各 NETADAPTER の親オブジェクトの中で、WDFDEVICE ごとの複数の NETADAPTER オブジェクトがあることができます。

ほとんどのネットワーク インターフェイス カード (NIC) ドライバーでは、物理デバイスの 1 つの NETADAPTER のみがあるが、複数のスロットは、サーバーの NIC を管理する場合、クライアント ドライバーによっては 1 つ以上の NETADAPTER にあります。 たとえば、[モバイル ブロード バンド WDF クラス拡張 (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)クライアント ドライバーが追加のパケット データ プロトコル (PDP) コンテキストを表す 1 つ以上の NETADAPTER オブジェクトを管理します。 

NETADAPTER オブジェクトは初期化され、クライアント ドライバーの内から作成する必要があります[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add
)コールバック関数を呼び出して[ **NetAdapterInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterinitallocate)と[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)します。 次に、その必要があります内から開始するドライバーの[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を呼び出して[ **NetAdapterStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). 呼び出しの前に**NetAdapterStart**ドライバーのリンク層の機能、電源機能、データパス機能など、アダプターの機能の設定、スケーリングが表示されることができます必要に応じて機能、およびハードウェア オフロード機能。

間のリレーションシップの詳細については、 [ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)、および[ **NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment) 、オブジェクトを参照してください[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)します。 詳細については**NET_RING** 、オブジェクトを参照してください[リングと net リングを行う反復子を Net](net-rings-and-net-ring-iterators.md)します。
