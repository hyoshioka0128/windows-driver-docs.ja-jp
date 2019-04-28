---
title: パケットの記述子と拡張機能
description: パケットの記述子と拡張機能
ms.assetid: 7B2357AE-F446-4AE8-A873-E13DF04D8D71
keywords:
- WDF ネットワーク アダプター クラスの拡張機能のパケットの記述子と拡張機能、NetAdapterCx データパス記述子では、複数のリング バッファー、NetAdapterCx パケット記述子、NetAdapterCx パケットの拡張機能
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 250eaa4e0c5e6657a04d61f57b59f0c739d7429d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375425"
---
# <a name="packet-descriptors-and-extensions"></a>パケットの記述子と拡張機能

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx で*パケット記述子*は構造体に小さな、compact、ランタイム拡張可能なネットワーク パケットをについて説明します。 各パケットでは、次の項目が必要です。

- 1 つのコア記述子 
- 1 つまたは複数のフラグメント記述子
- 0 個以上のパケットの拡張機能 

*記述子をコア*のパケットは、 [ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)構造体。 特定のパケットとパケットの最初のフラグメント記述子のインデックスのフレームのレイアウトなど、すべてのパケットに適用できる最も基本的なメタデータのみが含まれています。   

各パケットが、1 つまたは複数必要も*記述子をフラグメント*、または[ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)システム メモリ内の場所を記述する構造体で、パケットデータが存在します。

*パケットの拡張機能*オプションで、シナリオに固有の機能をパケット単位でメタデータを保持します。 たとえば、拡張機能が大量送信オフロード (LSO) チェックサム オフロード情報の保持し、セグメントの要素 (RSC) が表示されるか、アプリケーション固有の詳細を保持できます。

同時に、これらの記述子と拡張機能は、ネットワーク パケットに関するすべてのメタデータを保持します。 ここでは、2 つの例のパケットについて説明します。 最初の図は、パケット全体は 1 つのメモリ フラグメント内に格納し、チェックサム オフロード シナリオがオンにされましたを示しています。

![1 つのフラグメントのパケットのレイアウト](images/packet_layout_1_extension_1_fragment.png)

2 番目の図は、両方の RSC のメモリの 2 つのフラグメントに格納されているパケットと、チェックサム オフロードを有効になっています。

![2 つのフラグメントのパケットのレイアウト](images/packet_layout_2_extensions_2_fragments.png)


## <a name="packet-descriptor-storage-and-access"></a>パケット記述子の格納とアクセス

パケット記述子とフラグメントの記述子が両方に格納されている**NET_RING**構造体。 NIC のクライアント ドライバーでは、net のリングにアクセスし、により、ハードウェアへのネットワーク データを投稿し、完成したデータは、OS をドレインする NetAdapterCx を使用する Net リング反復子インターフェイスを呼び出すことによってそれらの操作を実行します。 

Net のリングとネットの反復子インターフェイスのリングの詳細については、次を参照してください。[リングと net リングを行う反復子を Net](net-rings-and-net-ring-iterators.md)します。

## <a name="packet-descriptor-extensibility"></a>パケットの記述子の機能拡張

機能拡張は、記述子の versionability とパフォーマンスの基盤を形成 NetAdapterCx パケット記述子のコア機能です。 、実行時に、オペレーティング システムは、利用拡張機能と共に、連続したブロックでは、各パケット キューのすべてのパケットの記述子を割り当てます。 拡張機能の各ブロックは、次の図に示すように、core 記述子の背後にすぐには。

![NetAdapterCx パケット記述子のレイアウト](images/packet-descriptors-1-layout.png)

NIC のクライアント ドライバーは使用できませんハードコーディングする任意の拡張機能のブロックのオフセット。 代わりに、オフセットを特定の拡張機能の実行時にクエリを実行する必要があります。 たとえば、ドライバーは、拡張 B へのオフセットをクエリし、70 のバイトのように、次の図に戻る。

![Core パケットの記述子の拡張機能へのオフセットのクエリを実行します。](images/packet-descriptors-2-offset-query.png)

パケット キューとその記述子が作成されると、そのすべての拡張機能のオフセットは、システムの定数、ドライバーは、多くの場合、オフセットを再クエリする必要はありませんのでが保証されます。 さらに、すべての拡張機能は、パケットのキューの初期化時にブロックでシステムによってあらかじめ割り当てられ、ため必要はありませんの具体的な記述子のリストの検索またはすべてのパケットへのポインターを格納することは、ブロックの実行時の割り当て拡張機能。

## <a name="packet-descriptor-versionability"></a>パケット記述子 versionability

NetAdapterCx の core パケット記述子簡単に拡張できます将来のリリースによって次の図のように、末尾に新しいフィールドの追加。

![NetAdapterCx core パケットの記述子のバージョン管理](images/packet-descriptors-3-core-descriptor-versioning.png)

古い V1 専用ドライバーはかを理解しているフィールドにアクセスできるように、V2 のフィールドをスキップする拡張機能のオフセットを使用して、V2 フィールドに新しいクライアント ドライバーにアクセスできます。 さらに、次の図に示すよう、各拡張機能は、同じ方法でバージョン管理できます。

![NetAdapterCx パケットの拡張機能のバージョン管理](images/packet-descriptors-4-extension-versioning.png)

新しい拡張機能を理解しているクライアント ドライバーを使用できます。 その他のクライアント ドライバーは、新しいフィールドをスキップできます。 これにより、個別にバージョンを更新するのには、パケット記述子のさまざまな部分です。

## <a name="packet-descriptors-and-datapath-performance"></a>パケット記述子とデータパス パフォーマンス

記載されている拡張機能は以前は capabable Nic のパフォーマンス要件を満たしているクライアント ドライバーのために、特典を提供しますギガビット/秒、何千ものキューの数百の。

1. パケットの記述子が保持されるコンパクト機能と使用されていない拡張機能は、0 バイトの記述子の領域を占めるように、CPU キャッシュ ヒット数を改善することになっています。 
2. ポインターの逆参照、オフセット演算のみ拡張機能は、インラインだけでなく領域を節約しますが、CPU キャッシュ ヒット数のことができますのではありません。 
3. 拡張機能は、ドライバーは、割り当てとアクティブなデータ パス内のメモリの割り当てを解除またはルック アサイド リストのコンテキストのブロックを処理する必要はありませんので、キューの作成時に割り当てられます。

## <a name="using-packet-extensions"></a>パケットの拡張機能の使用 

> [!IMPORTANT]
> 現時点では、クライアント ドライバーに限定[オペレーティング システムで定義された既存のパケットの拡張機能](#predefined-packet-extension-constants-and-helper-methods)します。

### <a name="registering-packet-extensions"></a>パケットの拡張機能を登録します。

NIC は、クライアント ドライバーのパケットの拡張機能を使用する最初の手順、サポートされているハードウェア オフロードを宣言することです。 チェックサムおよび LSO などのオフロードのサポートを提供する場合 NetAdapterCx は自動的に関連付けられているパケットの拡張機能を自動的に登録します。

広告のハードウェアのコード例は、のチェックサムおよび LSO オフロードを参照してください[NetAdapterCx ハードウェア オフロード](netadaptercx-hardware-offloads.md)します。

### <a name="querying-packet-extension-offsets-for-datapath-queues"></a>データパス キューのオフセットをパケットの拡張機能のクエリを実行します。

ご使用のハードウェアを宣言することで登録のパケットの拡張機能は、サポートをオフロード、拡張機能のオフセットが、パケットを処理するときにそれぞれアクセスする必要があります。 中に、拡張機能のオフセットを照会するには、ドライバーからの呼び出しを減らすことし、パフォーマンスの向上を*EvtNetAdapterCreateTx (Rx) キュー*コールバック関数とストアのキューのコンテキストでのオフセットの情報。 

拡張機能のオフセットのクエリを実行して、キューのコンテキストに格納することの例は、次を参照してください。[送信および受信キュー](transmit-and-receive-queues.md)します。

### <a name="getting-packet-extensions-at-runtime"></a>実行時にパケットの拡張機能を取得します。

キューのコンテキストで、拡張機能のオフセットを保存した後はいつでも拡張機能の情報が必要なを使用してできます。 たとえば、呼び出すことができます、 [ **NetExtensionGetPacketChecksum** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/nf-checksum-netextensiongetpacketchecksum)メソッド記述子が送信キューのハードウェアをプログラムします。

```C++
    // Get the extension offset from the device context
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);
    NET_EXTENSION checksumExtension = queueContext->ChecksumExtension;

    // Get the checksum info for this packet
    NET_PACKET_CHECKSUM* checksumInfo = NetExtensionGetPacketChecksum(checksumExtension, packetIndex);

    // Do work with the checksum info
    if (packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_NO_OPTIONS ||
        packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_WITH_OPTIONS ||
        packet->Layout.Layer3Type == NET_PACKET_LAYER3_TYPE_IPV4_UNSPECIFIED_OPTIONS)
    {
        if(checksumInfo->Layer4 == NET_PACKET_TX_CHECKSUM_REQUIRED)
        {
            ...
        }
    }
    ...
```

## <a name="predefined-packet-extension-constants-and-helper-methods"></a>定義済みのパケットの拡張機能の定数とヘルパー メソッド

NetAdapterCx では、既知のパケットの拡張機能の定数の定義を提供します。

| 定数 | 定義 |
| --- | --- |
| NET_PACKET_EXTENSION_INVALID_OFFSET | 無効なオフセット サイズから保護します。 |
| <ul><li>NET_PACKET_EXTENSION_CHECKSUM_NAME</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1_SIZE</li></ul> | 名前、バージョン、および checksum のパケットの拡張機能のサイズ。 |
| <ul><li>NET_PACKET_EXTENSION_LSO_NAME</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1_SIZE</li></ul> | 名前、バージョン、およびサイズの大きいオフロード (LSO) パケットの拡張機能を送信します。 |
| <ul><li>NET_PACKET_EXTENSION_RSC_NAME</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1_SIZE</li></ul> | 名前、バージョン、およびセグメントの要素 (RSC) パケットを受信する拡張機能のサイズ。 |

さらに、NetAdapterCx はラッパーとして機能する 3 つのヘルパー メソッドを提供します。、 [ **NetExtensionGetData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extension/nf-extension-netextensiongetdata)メソッド。 これらの各メソッドは、構造体の適切な型にポインターを返します。

| メソッド | 構造体 |
| --- | --- |
| [**NetExtensionGetPacketChecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/nf-checksum-netextensiongetpacketchecksum) | [**NET_PACKET_CHECKSUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksumtypes/ns-checksumtypes-_net_packet_checksum) |
| [**NetExtensionGetLargeSendSegmentation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lso/nf-lso-netextensiongetpacketlargesendsegmentation) | [**NET_PACKET_LARGE_SEND_SEGMENTATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lsotypes/ns-lsotypes-_net_packet_large_send_segmentation)
| [**NetExtensionGetPacketReceiveSegmentCoalescence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsc/nf-rsc-netextensiongetpacketreceivesegmentcoalescence) | [**NET_PACKET_RECEIVE_SEGMENT_COALESCENCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsctypes/ns-rsctypes-_net_packet_receive_segment_coalescence) |
