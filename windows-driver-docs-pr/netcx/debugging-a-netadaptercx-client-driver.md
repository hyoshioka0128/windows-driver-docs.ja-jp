---
title: NetAdapterCx クライアント ドライバーのデバッグ
description: NetAdapterCx クライアント ドライバーのデバッグ
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- デバッグ NetAdapterCx クライアント ドライバー、NetAdapterCx クライアント ドライバーのデバッグ
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d51cadcdc719e668af8f983473685fa4dd456363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323606"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーのデバッグ

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

使用することができます[Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff551876)コマンドには、クライアント ドライバーをデバッグします。  さらに、 [! ndiskd.netadapter](https://msdn.microsoft.com/library/windows/hardware/mt799821)アダプターのネットワーク固有のプロパティが表示されます。

また、使用することができます、`!ndiskd.netrb`デバッガー拡張機能のアドレスを持つ、 [ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)パケットとリング バッファー内のフラグメントを確認する構造体。  このコマンドでは、OS によって所有されているパケットの数と、クライアントによって所有されているパケットの数と共に、リング バッファー内の要素の数などの追加情報を示します。

以下を使用することができます。 NetAdapterCx クライアント ドライバーで ndiskd コマンド。

*  [**!ndiskd.cxadapter**](https://msdn.microsoft.com/library/windows/hardware/mt808786)
    *  NETADAPTER ハンドルを指定するには、NETADAPTER オブジェクトに関する情報を表示します。
*  [**!ndiskd.netqueue**](https://msdn.microsoft.com/library/windows/hardware/mt808789)
    *  NETTXQUEUE または NETRXQUEUE ハンドルを指定すると、データ パスのキューに関する情報を表示します。
*  [**!ndiskd.netrb**](https://msdn.microsoft.com/library/windows/hardware/mt808790)
    *  表示[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)情報。
*  [**!ndiskd.netpacket**](https://msdn.microsoft.com/library/windows/hardware/mt808787)
    *  に関する情報が表示されます、 [ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)します。
*  [**!ndiskd.netpacketfragment**](https://msdn.microsoft.com/library/windows/hardware/mt808788)
    *  に関する情報が表示されます、 [ **NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)します。
