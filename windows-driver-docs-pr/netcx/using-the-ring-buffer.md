---
title: リング バッファーの使用
description: リング バッファーの使用
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- リング バッファーを使用して NetAdapterCx、NetCx、リング バッファーを使用して NetAdapterCx PCI デバイス リング バッファーを NetAdapterCx 非同期 I/O
ms.date: 03/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50cf916654fcf6853029454808174b583a05476e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580125"
---
# <a name="using-the-ring-buffer"></a>リング バッファーの使用

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

A [ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)は 1 つ以上の循環バッファー [ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet) NetAdapterCx 間で共有される構造と、クライアント。 キューのパケットのリング バッファーにアクセスするに最初に呼び出す**NetRx (テキサス州) QueueGetDatapathDescriptor**キューのデータパス記述子構造体を取得するを呼び出すし、 [NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)マクロをリング バッファーを取得します。

パケットのリング バッファー内の各要素には、クライアント ドライバーまたは NetAdapterCx が所有します。 インデックス メンバーの値は、所有権を制御します。 具体的には、クライアント ドライバーはからのすべての要素を所有している**BeginIndex**に**EndIndex - 1**包括的です。

たとえば場合、 **BeginIndex** 2 と**EndIndex**が 5 の場合、クライアント ドライバーは、3 つの要素を所有している。 2、3、および 4 のインデックス値を持つ要素。
場合**BeginIndex**と等しい**EndIndex**、クライアント ドライバーが任意の要素を所有していません。

増分することで、リング バッファーに要素が追加 NetAdapterCx **EndIndex**します。 クライアント ドライバーが増分することで、要素の所有権を返します**BeginIndex**します。

クライアント ドライバーが必要に応じて設定**NextIndex**をハードウェアに送信される、次のパケットのインデックス。

![リング バッファーを使用して](images/using-the-ring-buffer.gif "リング バッファーを使用して")

このモデルで、クライアントの間でのインデックス値を持つパケットが送信**BeginIndex**と**NextIndex - 1**ハードウェアを包括的な。 インデックス値を持つパケット**NextIndex**と**EndIndex - 1**クライアントによって所有されますが、ハードウェアにまだ送信されていません。 場合の値**BeginIndex**がの値と等しい**NextIndex**ハードウェアにすべてのパケットをしないプログラムは、クライアント。

送信またはデータを受け取ると、ハードウェア、クライアントは次のように進めます。 **BeginIndex** NetAdapterCx にパケットの所有権を転送します。 クライアントは、入力候補を使用してパケットを追跡する場合、**完了**フラグ**NET_PACKET_FRAGMENT**、クライアントが呼び出すことができます[ **NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)を進める**BeginIndex**完了した各パケットで自動的にします。

リング バッファーが循環のため、最終的にインデックス値はバッファーの末尾をラップし、先頭に戻っています。 リング バッファーのインデックスを増分する場合は、ラップを処理するには、呼び出す[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)します。

## <a name="pci-device-drivers"></a>PCI デバイス ドライバー

通常、ハードウェア レベル (たとえば、一般的な PCI Nic) でのリング バッファーを使用しているデバイスのドライバーの操作、 [ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)直接のインデックス。

PCI デバイス ドライバーの一般的な流れを次に示します。

1. 呼び出す[ **NetRxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuegetdatapathdescriptor)または[ **NetTxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuegetdatapathdescriptor)キューのデータパスを取得するには記述子。 これは、ドライバーからの呼び出しを減らすことに、キューのコンテキストの領域に格納できます。
2. データパス記述子を使用して呼び出すことによってキューのパケットのリング バッファーを取得する[NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)します。
3. プログラムのリング バッファーのまでループでのハードウェアにパケット**NextIndex** equals **EndIndex**:
    1. 呼び出す[ **NetRingBufferGetPacketAtIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetpacketatindex)で**NextIndex**します。
    2. 変換、 **NET_PACKET**記述子に関連付けられたハードウェア パケットの記述子。
    3. 呼び出す[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)します。
4. までループでパケットを完了**BeginIndex** equals **NextIndex**または不完全なパケットに達するまで。
    1. 呼び出す[ **NetRingBufferGetPacketAtIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetpacketatindex)で**BeginIndex**します。
    2. 関連付けられたハードウェア記述子が入力候補を示すかどうかを検出します。 それ以外の場合は、終了します。
    3. ハードウェアの記述子を変換、 [ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)します。
    4. 呼び出す[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)します。

## <a name="device-drivers-with-asynchronous-io"></a>デバイス ドライバーの非同期 I/O

非同期の I/O モデルでは、USB などのデバイスを対象とするクライアント ドライバーの中に変更することも、 [ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)インデックスを直接代わりに使用をお勧めするより高いレベルのルーチン注文入力候補を管理するには。

* [**NetRingBufferAdvanceNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferadvancenextpacket)
* [**NetRingBufferGetNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetnextpacket)
* [**NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)

非同期 i/o デバイス ドライバーの一般的な流れを次に示します。

1. 呼び出す[ **NetRxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuegetdatapathdescriptor)または[ **NetTxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuegetdatapathdescriptor)キューのデータパスを取得するには記述子。
2. データパス記述子を使用して呼び出すことによってキューのパケットのリング バッファーを取得する[NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)します。
3. リング バッファーにパケットを反復処理します。 通常、ループでは、次の操作を行います。
    1. 呼び出す[ **NetRingBufferGetNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetnextpacket)します。
    2. 送信または受信をハードウェアをプログラムします。 これは、非同期 I/O を開始します。
    3. 呼び出す[ **NetRingBufferAdvanceNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferadvancenextpacket)します。
4. 呼び出す[ **NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)します。

非同期 I/O の完了とクライアントの設定、**完了**最初のフラグが関連付けられている[ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)に**TRUE**. これにより、 [ **NetRingBufferReturnCompletedPackets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)パケットを完了します。 関連付けられている、最初にアクセスする**NET_PACKET_FRAGMENT** 、パケットの呼び出し、 [NET_PACKET_GET_FRAGMENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_packet_get_fragment)パケットでキューのデータパス記述子では、マクロ、 *0*パラメーターのインデックスを作成します。
