---
title: NetAdapterCx クライアント ドライバーのデバッグ
description: NetAdapterCx クライアント ドライバーのデバッグ
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- デバッグ NetAdapterCx クライアント ドライバー、NetAdapterCx クライアント ドライバーのデバッグ
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1358a2504b85c4516b6f597b7712c7548611b355
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386363"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーのデバッグ

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

使用することができます[Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)コマンドには、クライアント ドライバーをデバッグします。  さらに、 [! ndiskd.netadapter](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netadapter)アダプターのネットワーク固有のプロパティが表示されます。

また、使用することができます、`!ndiskd.netrb`デバッガー拡張機能のアドレスを持つ、 [ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)パケットとリング バッファー内のフラグメントを確認する構造体。  このコマンドでは、OS によって所有されているパケットの数と、クライアントによって所有されているパケットの数と共に、リング バッファー内の要素の数などの追加情報を示します。

以下を使用することができます。 NetAdapterCx クライアント ドライバーで ndiskd コマンド。

*  [ **!ndiskd.cxadapter**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-cxadapter)
    *  NETADAPTER ハンドルを指定するには、NETADAPTER オブジェクトに関する情報を表示します。
*  [ **!ndiskd.netqueue**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netqueue)
    *  NETTXQUEUE または NETRXQUEUE ハンドルを指定すると、データ パスのキューに関する情報を表示します。
*  [ **!ndiskd.netrb**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netrb)
    *  表示[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)情報。
*  [ **!ndiskd.netpacket**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacket)
    *  に関する情報が表示されます、 [ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)します。
*  [ **!ndiskd.netpacketfragment**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacketfragment)
    *  に関する情報が表示されます、 [ **NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)します。
