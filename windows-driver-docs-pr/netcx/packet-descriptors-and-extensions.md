---
title: パケットの記述子と拡張機能
description: パケットの記述子と拡張機能
ms.assetid: 7B2357AE-F446-4AE8-A873-E13DF04D8D71
keywords:
- WDF ネットワーク アダプター クラスの拡張機能のパケットの記述子と拡張機能、NetAdapterCx データパス記述子では、複数のリング バッファー、NetAdapterCx パケット記述子、NetAdapterCx パケットの拡張機能
ms.date: 07/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08b351ab2f6bc9b6787b9cd835139ea06890ae93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577865"
---
# <a name="packet-descriptors-and-extensions"></a>パケットの記述子と拡張機能

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx で*パケット記述子*は構造体に小さな、compact、ランタイム拡張可能なネットワーク パケットをについて説明します。 各パケットでは、次の項目が必要です。

- 1 つのコア記述子 
- 1 つまたは複数のフラグメント記述子
- 0 個以上のパケットの拡張機能 

*記述子をコア*のパケットは、 [NET_PACKET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)構造体。 特定のパケットとパケットの最初のフラグメント記述子のインデックスのフレームのレイアウトなど、すべてのパケットに適用できる最も基本的なメタデータのみが含まれています。   

1 つまたは複数の各パケット必要がありますも*記述子のフラグメント*、または[NET_PACKET_FRAGMENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)パケット データが存在するシステム メモリ内の場所を記述する構造体。

*パケットの拡張機能*オプションで、シナリオに固有の機能をパケット単位でメタデータを保持します。 たとえば、拡張機能が大量送信オフロード (LSO) チェックサム オフロード情報の保持し、セグメントの要素 (RSC) が表示されるか、アプリケーション固有の詳細を保持できます。

同時に、これらの記述子と拡張機能は、ネットワーク パケットに関するすべてのメタデータを保持します。 ここでは、2 つの例のパケットについて説明します。 最初の図は、パケット全体は 1 つのメモリ フラグメント内に格納し、チェックサム オフロード シナリオがオンにされましたを示しています。

![1 つのフラグメントのパケットのレイアウト](images/packet_layout_1_extension_1_fragment.png)

2 番目の図は、両方の RSC のメモリの 2 つのフラグメントに格納されているパケットと、チェックサム オフロードを有効になっています。

![2 つのフラグメントのパケットのレイアウト](images/packet_layout_2_extensions_2_fragments.png)


## <a name="storage-of-packet-descriptors"></a>パケットの記述子のストレージ

Core 記述子とフラグメント記述子は、2 つの別のリング バッファー内のストアド indepenently、*パケット リング*と*フラグメント リング*します。 パケットのリング内のすべてのコア記述子が、そのパケットのフラグメントの記述子を検索するため、フラグメント リングへのインデックス。 別のデータ構造体、 [NET_DATAPATH_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/ns-netdatapathdescriptor-_net_datapath_descriptor)、グループ、パケットのリングとフラグメント リング パケット キューに分けます。

![複数のリングのレイアウト](images/multi-ring.png) 

すべてのパケットのキューには、独自[NET_DATAPATH_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/ns-netdatapathdescriptor-_net_datapath_descriptor)構造、および、その結果、独自のパケット リング フラグメント リング、およびそれらのリング内の記述子。 そのため、各パケット キューのネットワーク データ転送操作では完全に独立してます。 パケット キューの詳細については、[送信および受信キュー](transmit-and-receive-queues.md)を参照してください。

クライアント ドライバーは定義済みの便利なマクロを使用してパケット リング、フラグメントのリングが含まれている記述子にアクセスすることをお勧めします。 これらのマクロの詳細については、[リング バッファーを使用して](using-the-ring-buffer.md)を参照してください。

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

ご使用のハードウェアを宣言することで登録のパケットの拡張機能は、サポートをオフロード、拡張機能のオフセットが、パケットを処理するときにそれぞれアクセスする必要があります。 中に、拡張機能のオフセットを照会するには、ドライバーからの呼び出しを減らすことし、パフォーマンスの向上を*EvtNetAdapterCreateTx (Rx) キュー*コールバック関数とストアのキューのコンテキストでのオフセットの情報。 送信キューの例を示します。 この例は上の例のような*[EvtNetAdapterCreateTxQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)* が、パケットの拡張機能についてのみ説明します。

```C++
NTSTATUS
MyAdapterCreateTxQueue(
    _In_    NETADAPTER          Adapter,
    _Inout_ PNETTXQUEUE_INIT    TxQueueInit
)
{
    NTSTATUS status = STATUS_SUCCESS;

    // Prepare the configuration structure
    NET_PACKET_QUEUE_CONFIG txConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(
        &txConfig,
        EvtTxQueueAdvance,
        EvtTxQueueSetNotificationEnabled,
        EvtTxQueueCancel);

    // Configure other Tx queue properties such as packet contexts
    ...

    // Create the transmit queue
    NETPACKETQUEUE txQueue;
    status = NetTxQueueCreate(
        txQueueInit,
        &txAttributes,
        &txConfig,
        &txQueue);

    // Get the queue context for storing the queue ID and packet extension offset info
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);

    // Query checksum packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY extension;
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1);

    queueContext->ChecksumExtensionOffset = NetTxQueueGetPacketExtensionOffset(txQueue, &extension);

    // Query Large Send Offload packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_LSO_NAME,
        NET_PACKET_EXTENSION_LSO_VERSION_1);
    
    queueContext->LsoExtensionOffset = NetTxQueueGetPacketExtensionOffset(txQueue, &extension);

    return status;
}
```

### <a name="getting-packet-extensions-at-runtime"></a>実行時にパケットの拡張機能を取得します。

キューのコンテキストで、拡張機能のオフセットを保存した後はいつでも拡張機能の情報が必要なを使用してできます。 たとえば、呼び出すことができます、 [NetPacketGetPacketChecksum](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/nf-netpacket-netpacketgetpacketchecksum)メソッド記述子がハードウェアをプログラムします。

```C++
    // Get the extension offset from the device context
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);
    size_t checksumOffset = queueContext->ChecksumExtensionOffset;

    // Get the checksum info for this packet
    NET_PACKET_CHECKSUM* checksumInfo = NetPacketGetChecksum(packet, checksumOffset);

    // Do work with the checksum info
    if(checksumInfo->Layer4 == NET_PACKET_TX_CHECKSUM_REQUIRED)
    {
        ...
    }
```

## <a name="predefined-packet-extension-constants-and-helper-methods"></a>定義済みのパケットの拡張機能の定数とヘルパー メソッド

NetAdapterCx では、既知のパケットの拡張機能の定数の定義を提供します。

| 定数 | 定義 |
| --- | --- |
| NET_PACKET_EXTENSION_INVALID_OFFSET | 無効なオフセット サイズから保護します。 |
| <ul><li>NET_PACKET_EXTENSION_CHECKSUM_NAME</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1_SIZE</li></ul> | 名前、バージョン、および checksum のパケットの拡張機能のサイズ。 |
| <ul><li>NET_PACKET_EXTENSION_LSO_NAME</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1_SIZE</li></ul> | 名前、バージョン、およびサイズの大きいオフロード (LSO) パケットの拡張機能を送信します。 |
| <ul><li>NET_PACKET_EXTENSION_RSC_NAME</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1_SIZE</li></ul> | 名前、バージョン、およびセグメントの要素 (RSC) パケットを受信する拡張機能のサイズ。 |

さらに、NetAdapterCx はラッパーとして機能する 3 つのヘルパー メソッドを提供します。、 [NetPacketGetExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/nf-netpacket-netpacketgetextension)メソッド。 これらの各メソッドは、構造体の適切な型にポインターを返します。

| メソッド | 構造体 |
| --- | --- |
| [NetPacketGetPacketChecksum](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/nf-netpacket-netpacketgetpacketchecksum) | [NET_PACKET_CHECKSUM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_checksum) |
| [NetPacketGetPacketLargeSendSegmentation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/nf-netpacket-netpacketgetpacketlargesendsegmentation) | [NET_PACKET_LARGE_SEND_SEGMENTATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_large_send_segmentation)
| [NetPacketGetPacketReceiveSegmentCoalescence](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/nf-netpacket-netpacketgetpacketreceivesegmentcoalescence) | [NET_PACKET_RECEIVE_SEGMENT_COALESCENCE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_receive_segment_coalescence) |
