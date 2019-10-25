---
title: NetAdapterCx オブジェクトの概要
description: NetAdapterCx オブジェクトの概要
ms.assetid: 1635C737-42C6-4957-A3E0-1184A5545441
keywords:
- NetAdapterCx オブジェクトの概要、オブジェクトの NetCx 概要
ms.date: 11/01/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b85201bcf93dbf2a2ff2a45840d95d8a06a4a20d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838269"
---
# <a name="summary-of-netadaptercx-objects"></a>NetAdapterCx オブジェクトの概要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

次の図は、NetAdapterCx オブジェクトの既定の親子関係を示しています。 親オブジェクトは、図の最上部にあります。たとえば、NETADAPTER オブジェクトは既定では WDFDEVICE オブジェクトの子です。 複数のインスタンスを持つことができるオブジェクトは、2つのボックスで示されます。

![NetAdapterCx クライアントドライバーの NetAdapterCx オブジェクトの概要](images/netcx-adapter-object-model.png "NetAdapterCx クライアントドライバーの NetAdapterCx オブジェクトの概要")

WDFDEVICE オブジェクトは、デバイスを表す標準[フレームワークオブジェクト](../wdf/wdf-objects.md)です。 NETADAPTER オブジェクトは、すべてのネットワーク i/o のエンドポイントであるネットワークインターフェイスを表します。 Wdfdevice は、各 NETADAPTER の親オブジェクトである WDFDEVICE に対して複数の NETADAPTER オブジェクトを持つことができます。

ほとんどのネットワークインターフェイスカード (NIC) ドライバーでは、物理デバイスに対して1つの NETADAPTER しか使用できませんが、複数のスロットがあるサーバー NIC を管理しているクライアントドライバーもあります。 例として、 [Mobile ブロードバンド WDF Class Extension (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)クライアントドライバーでは、それぞれが追加のパケットデータプロトコル (PDP) コンテキストを表す複数の netadapter オブジェクトを管理する場合があります。 

NETADAPTER オブジェクトは、 [**NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterinitallocate)および[**NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)を呼び出すことによって、クライアントドライバーの[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) callback 関数内から初期化および作成する必要があります。 次に、 [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出して、ドライバーの[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) callback 関数内から開始する必要があります。 **NetAdapterStart**を呼び出す前に、ドライバーは必要に応じて、リンクレイヤー機能、電源機能、データパス機能、受信スケーリング機能、ハードウェアオフロード機能などのアダプターの機能を設定できます。

[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)オブジェクトと[**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)オブジェクトの関係の詳細については、「[パケット記述子と拡張機能](packet-descriptors-and-extensions.md)」を参照してください。 **NET_RING**オブジェクトの詳細については、「 [net リングと net RING 反復子](net-rings-and-net-ring-iterators.md)」を参照してください。
