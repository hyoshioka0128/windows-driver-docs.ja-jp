---
title: ネットワーク データ バッファーの管理
description: ネットワーク データ バッファーの管理
ms.assetid: BFE1D376-88FB-41CB-AB6D-A0D6BB83128C
keywords:
- WDF ネットワークアダプタークラス拡張バッファーマネージャー, ネットワークデータバッファー管理
ms.date: 02/20/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 89f9cd1ea75ab39f9989dabb6c0e6052a78ba0be
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209023"
---
# <a name="network-data-buffer-management"></a>ネットワーク データ バッファーの管理

バッファー管理は、ネットワークインターフェイスカード (NIC) クライアントドライバーとオペレーティングシステムを連携させる機能です。この機能を使用すると、送信 (Tx) および受信 (Rx) データパスのシステムメモリからパケットデータバッファーを割り当てることができます。 これにより、NIC のパフォーマンスが向上し、NIC のクライアントドライバーのメモリ有効期間の管理が容易になり、メモリのシステムをより細かく制御できるようになります。

## <a name="the-benefits-of-buffer-management-in-netadaptercx"></a>NetAdapterCx でのバッファー管理の利点

パケットペイロードのシステムメモリからデータバッファーが割り当てられる場所の選択は、データパスのパフォーマンスにとって重要です。 NetAdapterCx では、バッファー管理モデルは DMA 対応の NIC ハードウェア用に最適化されています。また、クライアントドライバーが利用できる最適な方法は、システムが送信パスと Rx パスの両方に代わってデータバッファーを割り当てられるようにすることです。 ただし、クライアントドライバーは、クライアントのハードウェアで簡単に使用できるように、データバッファーの割り当てと方法に影響を与える可能性があります。 

たとえば、一般的な DMA 対応 NIC について考えてみましょう。 このアプローチには、次のような利点があります。

1. データバッファーが割り当てられ、システムによって解放されます。 そのため、クライアントドライバーは、メモリの有効期間管理の負荷から解放されます。
2. システムは、割り当てられたデータバッファーが、クライアントドライバーによって宣言された機能に基づいて、NIC ハードウェアに対して DMA 対応であることを確認します。 その後、クライアントドライバーは、追加の DMA マッピング操作を実行することなく、単にデータバッファーをそのままの状態でプログラムによってプログラムすることができます。
3. システムは、データバッファーを割り当てるときに、上位層アプリケーションのニーズを考慮に入れることができるため、ローカルのエンドツーエンドのパフォーマンスだけでなく、グローバルなエンドツーエンドのパフォーマンスを最適化することを決定できます。

USB ベースのネットワークドングルや、その他の拡張/ソフトウェア Nic のような非 DMA の機能の場合、バッファー管理モデルでは、データバッファー管理をクライアントドライバーに対して完全に終了するオプションも提供されます。 

## <a name="how-to-leverage-buffer-management"></a>バッファー管理を活用する方法

> [!IMPORTANT]
> お使いのハードウェアが DMA に対応している場合は、Rx および Tx の機能を設定する前に、WDFDMAENABLER オブジェクトを作成する必要があります。 [**WDF_DMA_ENABLER_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)構造で WDFDMAENABLER オブジェクトを構成する場合は、 **Wdmdmaversionoverride**メンバーを**3**に設定して、DMA バージョン3を指定するようにしてください。

バッファー管理をオプトインするには、次の手順を実行します。

1. [**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す前に、ネットアダプターを起動するときに、RX パスと TX パスの[**NET_ADAPTER_RX_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_rx_capabilities)と[**NET_ADAPTER_TX_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_tx_capabilities)データ構造を使用して、ハードウェアのデータバッファー機能と制約についてシステムに指示します。 
2. 初期化関数のいずれかを呼び出すことによって、2つの機能構造を初期化します。 たとえば、DMA 対応の NIC クライアントドライバーは、 [**NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_tx_capabilities_init_for_dma)と[**NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED_DMA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_rx_capabilities_init_system_managed_dma)を使用して、ハードウェア DMA capablities を宣言し、データバッファーを自動的に管理するようにシステムに指示します。
3. 初期化された Tx および Rx 機能の構造体を[**NetAdapterSetDatapathCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)メソッドに渡します。


## <a name="example"></a>例

次の例は、NIC クライアントドライバーでバッファーマネージャーの使用を開始する方法について、前のセクションで説明した基本的な手順を示しています。 この例では、Tx と Rx の両方に DMA を使用しているため、以前はデバイスコンテキスト空間に格納されている WDFDMAENABLER オブジェクトが作成されていました。 

この例では、Tx および Rx 機能の構造体を初期化した後に、フラグメントバッファーに関するヒントもいくつか設定します。 これらのヒントは、パフォーマンスを向上させるために、NetAdapterCx ドライバーとプロトコルドライバーで使用できます。

わかりやすくするために、エラー処理は省略されています。

```C++
VOID
MyAdapterSetDatapathCapabilities(
    _In_ NETADAPTER Adapter
)
{
    // Get the device context
    PMY_DEVICE_CONTEXT deviceContext = GetMyContextFromDevice(Adapter);

    // Set various capabilities such as link layer MTU size, link layer capabilities, and power capabilities
    ...   

    // Initialize the Tx DMA capabilities structure
    NET_ADAPTER_DMA_CAPABILITIES txDmaCapabilities;
    NET_ADAPTER_DMA_CAPABILITIES_INIT(&txDmaCapabilities,
                                      deviceContext->dmaEnabler);

    // Set Tx capabilities
    NET_ADAPTER_TX_CAPABILITIES txCapabilities;
    NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA(&txCapabilities,
                                             &txDmaCapabilities,
                                             MAX_PACKET_SIZE,
                                             1);
    txCapabilities.FragmentRingNumberOfElementsHint = deviceContext->NumTransmitControlBlocks * MAX_PHYS_BUF_COUNT;
    txCapabilities.MaximumNumberOfFragments = MAX_PHYS_BUF_COUNT;

    // Initialize the Rx DMA capabilities structure
    NET_ADAPTER_DMA_CAPABILITIES rxDmaCapabilities;
    NET_ADAPTER_DMA_CAPABILITIES_INIT(&rxDmaCapabilities,
                                      deviceContext->dmaEnabler);

    // Set Rx capabilities
    NET_ADAPTER_RX_CAPABILITIES rxCapabilities;
    NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED_DMA(&rxCapabilities,
                                                        &rxDmaCapabilities,
                                                        MAX_PACKET_SIZE + FRAME_CRC_SIZE + RSVD_BUF_SIZE,
                                                        1);
    rxCapabilities.FragmentBufferAlignment = 64;
    rxCapabilities.FragmentRingNumberOfElementsHint = deviceContext->NumReceiveBuffers;

    // Set the adapter's datapath capabilities
    NetAdapterSetDatapathCapabilities(Adapter, 
                                      &txCapabilities, 
                                      &rxCapabilities);
}
```
