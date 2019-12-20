---
title: パケットの記述子と拡張機能
description: パケットの記述子と拡張機能
ms.assetid: 7B2357AE-F446-4AE8-A873-E13DF04D8D71
keywords:
- WDF ネットワークアダプタークラス拡張パケット記述子と拡張機能、NetAdapterCx データパス記述子、マルチリングバッファー、NetAdapterCx パケット記述子、NetAdapterCx パケット拡張機能
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: c34a3f491f7c16c315c24455bc984f77e9025035
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209037"
---
# <a name="packet-descriptors-and-extensions"></a>パケットの記述子と拡張機能

NetAdapterCx では、*パケット記述子*は、ネットワークパケットを記述する、小さい、コンパクト、ランタイム拡張可能な構造です。 各パケットには次のものが必要です。

- 1つのコア記述子 
- 1つまたは複数のフラグメント記述子
- 0個以上のパケット拡張 

パケットの*コア記述子*は[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)構造体です。 これには、特定のパケットのフレーミングレイアウトや、パケットの最初のフラグメント記述子へのインデックスなど、すべてのパケットに適用される最も基本的なメタデータのみが含まれます。   

各パケットには、パケットデータが存在するシステムメモリ内の場所を記述する1つまたは複数の*フラグメント記述子*( [**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)構造) も必要です。

*拡張*機能は省略可能で、シナリオ固有の機能に対して、パケット単位またはフラグメントごとのメタデータを保持します。 たとえば、パケット拡張では、checksum、large send offload (LSO)、および receive segment 要素 (RSC) のオフロード情報を保持することも、アプリケーション固有の詳細を保持することもできます。 フラグメント拡張機能は、仮想アドレス情報、論理 DMA アドレス情報、またはフラグメントのその他の情報を保持できます。

これらの記述子と拡張機能は、ネットワークパケットに関するすべてのメタデータを保持します。 ここでは、パケットを記述する方法の2つの例を示します。 最初の図は、パケット全体が単一のメモリフラグメント内に格納され、チェックサムオフロードが有効になっているシナリオを示しています。

![1フラグメントのパケットレイアウト](images/packet_layout_1_extension_1_fragment.png)

2番目の図は、RSC とチェックサムオフロードの両方が有効になっている2つのメモリフラグメントに格納されているパケットを示しています。

![2フラグメントのパケットレイアウト](images/packet_layout_2_extensions_2_fragments.png)


## <a name="packet-descriptor-storage-and-access"></a>パケット記述子のストレージとアクセス

パケット記述子とフラグメント記述子は、どちらも**NET_RING**構造体に格納されます。 NIC クライアントドライバーは、net リング反復子インターフェイスを呼び出すことによって、ネットリングにアクセスし、それらに対して操作を実行します。これにより、ドライバーは NetAdapterCx を使用してネットワークデータをハードウェアにポストし、完了したデータを OS にドレインできます。 

ネットリングと Net Ring 反復子インターフェイスの詳細については、「 [net リングの概要](introduction-to-net-rings.md)」を参照してください。

## <a name="packet-descriptor-extensibility"></a>パケット記述子の拡張性

拡張性は、NetAdapterCx パケット記述子の中核となる機能であり、記述子の versionability 機能とパフォーマンスの基礎を形成します。 実行時には、オペレーティングシステムによって、各パケットキューのすべてのパケット記述子が、使用でき拡張機能と共に、連続するブロックに割り当てられます。 各拡張機能ブロックは、次の図に示すように、コア記述子のすぐ後ろに配置されます。

![NetAdapterCx パケット記述子のレイアウト](images/packet-descriptors-1-layout.png)

NIC クライアントドライバーは、任意の拡張ブロックへのオフセットをハードコーディングすることは許可されていません。 代わりに、特定の拡張機能へのオフセットに対して、実行時にクエリを実行する必要があります。 たとえば、ドライバーは、次の図に示すように、拡張 B へのオフセットをクエリし、70バイトを取得することがあります。

![コアパケット記述子の拡張機能へのオフセットのクエリ](images/packet-descriptors-2-offset-query.png)

パケットキューとその記述子が作成されると、すべての拡張オフセットがシステムによって一定であることが保証されるので、ドライバーはオフセットを頻繁に再クエリする必要がありません。 さらに、すべての拡張機能は、パケットキューの初期化時にシステムによって事前に割り当てられているため、ブロックの実行時割り当て、特定の記述子のリストの検索、またはすべてのパケットへのポインターの格納を必要としません。番号.

## <a name="packet-descriptor-versionability"></a>パケット記述子の versionability

NetAdapterCx のコアパケット記述子は、次の図に示すように、新しいフィールドを末尾に追加することで、将来のリリースで簡単に拡張できます。

![NetAdapterCx コアパケット記述子のバージョン管理](images/packet-descriptors-3-core-descriptor-versioning.png)

V2 フィールドを認識している新しいクライアントドライバーは、これらのフィールドにアクセスできますが、古い V1 専用ドライバーは拡張オフセットを使用して V2 フィールドをスキップします。これにより、認識しているフィールドにアクセスできるようになります。 また、次の図に示すように、各拡張機能は同じ方法でバージョン管理できます。

![NetAdapterCx パケット拡張のバージョン管理](images/packet-descriptors-4-extension-versioning.png)

新しい拡張機能を認識するクライアントドライバーで使用できます。 その他のクライアントドライバーは、新しいフィールドをスキップできます。 これにより、パケット記述子のさまざまな部分を個別にバージョン管理できます。

## <a name="packet-descriptors-and-datapath-performance"></a>パケット記述子とデータパスのパフォーマンス

前に説明した機能拡張機能は、クライアントドライバーが、1秒あたり数百ギガビット、数千のキューを持つ Nic のパフォーマンス要件を満たすのに役立つ利点を提供します。

1. 使用されていない機能と拡張機能では、記述子に0バイトの領域が占有されるため、パケット記述子はできるだけコンパクトに保持されます。 
2. ポインターの逆参照はありません。拡張がインラインであるため、オフセット算術演算のみが行われます。これにより、領域を節約できるだけでなく、CPU キャッシュヒットにも役立ちます。 
3. 拡張機能はキューの作成時に割り当てられるので、ドライバーは、アクティブなデータパスにメモリを割り当てたり割り当てを解除したり、コンテキストブロックのルックアサイドリストを処理したりする必要がありません。

## <a name="using-packet-extensions"></a>パケット拡張の使用 

> [!IMPORTANT]
> 現在、クライアントドライバーは、[オペレーティングシステムで定義されている既存のパケット拡張](#predefined-packet-extension-constants-and-helper-methods)に限定されています。

### <a name="registering-packet-extensions"></a>パケット拡張の登録

NIC クライアントドライバーでパケット拡張機能を使用するための最初の手順は、サポートされているハードウェアオフロードを宣言することです。 Checksum や LSO などのオフロードのサポートを提供する場合、NetAdapterCx は関連付けられているパケット拡張を自動的に登録します。

チェックサムと LSO のハードウェアオフロードのコード例については、「 [NetAdapterCx hardware オフロード](netadaptercx-hardware-offloads.md)」を参照してください。

### <a name="querying-packet-extension-offsets-for-datapath-queues"></a>データパスキューのパケット拡張のオフセットを照会しています

ハードウェアオフロードサポートを宣言してパケット拡張を登録した後は、パケットを処理する際にそれぞれにアクセスするための拡張オフセットが必要になります。 ドライバーからの呼び出しを減らしてパフォーマンスを向上させるには、 *EvtNetAdapterCreateTx (Rx) キュー*コールバック関数の間に拡張機能のオフセットを照会し、キューコンテキストにオフセット情報を格納します。 

拡張機能のオフセットに対してクエリを実行し、それをキューのコンテキストに格納する例については、「[キューの転送と受信](transmit-and-receive-queues.md)」を参照してください。

### <a name="getting-packet-extensions-at-runtime"></a>実行時のパケット拡張機能の取得

キューコンテキストに拡張オフセットを格納したら、拡張機能の情報が必要なときはいつでも使用できます。 たとえば、 [**Netextensiongetpacketchecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/nf-checksum-netextensiongetpacketchecksum)メソッドを呼び出して、送信キュー用にハードウェアの記述子をプログラミングすることができます。

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

## <a name="predefined-packet-extension-constants-and-helper-methods"></a>定義済みのパケット拡張定数とヘルパーメソッド

NetAdapterCx は、既知のパケット拡張定数の定義を提供します。

| 定数 | 定義 |
| --- | --- |
| NET_PACKET_EXTENSION_INVALID_OFFSET | 無効なオフセットサイズに対してガードを行います。 |
| <ul><li>NET_PACKET_EXTENSION_CHECKSUM_NAME</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1</li><li>NET_PACKET_EXTENSION_CHECKSUM_VERSION_1_SIZE</li></ul> | チェックサムパケット拡張の名前、バージョン、およびサイズ。 |
| <ul><li>NET_PACKET_EXTENSION_LSO_NAME</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1</li><li>NET_PACKET_EXTENSION_LSO_VERSION_1_SIZE</li></ul> | Large send offload (LSO) パケット拡張の名前、バージョン、およびサイズ。 |
| <ul><li>NET_PACKET_EXTENSION_RSC_NAME</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1</li><li>NET_PACKET_EXTENSION_RSC_VERSION_1_SIZE</li></ul> | 受信セグメントの要素 (RSC) パケット拡張の名前、バージョン、およびサイズ。 |

さらに、NetAdapterCx には、 [**Netextensiongetdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/extension/nf-extension-netextensiongetdata)メソッドのラッパーとして機能する3つのヘルパーメソッドが用意されています。 これらの各メソッドは、適切な構造体の型へのポインターを返します。

| メソッド | 構造体 |
| --- | --- |
| [**NetExtensionGetPacketChecksum**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksum/nf-checksum-netextensiongetpacketchecksum) | [**NET_PACKET_CHECKSUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/checksumtypes/ns-checksumtypes-_net_packet_checksum) |
| [**NetExtensionGetLso**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lso/nf-lso-netextensiongetpacketlso) | [**NET_PACKET_LSO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lsotypes/ns-lsotypes-_net_packet_lso)
| [**NetExtensionGetPacketRsc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsc/nf-rsc-netextensiongetpacketrsc) | [**NET_PACKET_RSC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rsctypes/ns-rsctypes-_net_packet_rsc) |
