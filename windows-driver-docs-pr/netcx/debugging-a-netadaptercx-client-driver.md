---
title: NetAdapterCx クライアント ドライバーのデバッグ
description: NetAdapterCx クライアント ドライバーのデバッグ
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- NetAdapterCx クライアントドライバーのデバッグ, NetAdapterCx クライアントドライバーのデバッグ
ms.date: 06/17/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 769698e26296355645940e52c5842105432a2e83
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593962"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>NetAdapterCx クライアント ドライバーのデバッグ

[Windows Driver Framework Extensions (Wdfkd.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)コマンドを使用して、クライアントドライバーをデバッグできます。  さらに、 [! ndiskd netadapter](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netadapter)には、アダプターのネットワーク固有のプロパティが表示されます。

また、 `!ndiskd.netrb` デバッガー拡張機能を[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)構造体のアドレスと共に使用して、リングバッファー内のパケットとフラグメントを調べることもできます。  このコマンドを実行すると、リングバッファー内の要素の数や、OS によって所有されているパケットの数、クライアントが所有するパケットの数などの追加情報が提供されます。

NetAdapterCx クライアントドライバーでは、次の! ndiskd コマンドを使用できます。

*  [**!ndiskd.cxadapter**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-cxadapter)
    *  NETADAPTER ハンドルを指定すると、NETADAPTER オブジェクトに関する情報が表示されます。
*  [**!ndiskd.netqueue**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netqueue)
    *  NETTXQUEUE ハンドルまたは NETRXQUEUE ハンドルを指定すると、データパスキューに関する情報が表示されます。
*  [**!ndiskd.netrb**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netrb)
    *  [**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)情報を表示します。
*  [**!ndiskd.netpacket**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacket)
    *  [**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)に関する情報を表示します。
*  [**! ndiskd netfragment**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netfragment)
    *  [**NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)に関する情報を表示します。
