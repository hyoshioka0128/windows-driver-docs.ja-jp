---
title: ネットワーク データ バッファーの管理
description: ネットワーク データ バッファーの管理
ms.assetid: BFE1D376-88FB-41CB-AB6D-A0D6BB83128C
keywords:
- WDF ネットワーク アダプター クラス拡張バッファー マネージャー、ネットワーク データ バッファー管理
ms.date: 02/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37a1fe52288bbb0e45666178573f861baac3be69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572160"
---
# <a name="network-data-buffer-management"></a>ネットワーク データ バッファーの管理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

バッファー管理は、ネットワーク インターフェイス カード (NIC) のクライアント ドライバーと、オペレーティング システム (テキサス州) の送信用のシステム メモリからのパケット データ バッファーの割り当てと共同で作業し、受信 (Rx) のデータ パスを可能にする機能です。 これにより、NIC のパフォーマンスを向上させる、NIC のクライアント ドライバーでは、メモリの有効期間管理をしやすくなりますし、メモリ経由でシステムの詳細に制御します。

## <a name="the-benefits-of-buffer-management-in-netadaptercx"></a>NetAdapterCx でバッファー管理の利点があります。

データ バッファーがパケットのペイロードのシステム メモリから割り当てられた場所の選択は、データ パスのパフォーマンスにとって重要です。 NetAdapterCx では、バッファー管理モデルは DMA 対応 NIC ハードウェアでは、最適化され、クライアント ドライバーに活用するために最適な方法は、テキサス州と Rx のパスの代わりにデータ バッファーを割り当てるシステム。 ただし、クライアント ドライバーがどこに影響を与えるし、システムがデータを割り当てる方法をバッファーするため、クライアントのハードウェアによって簡単に使用することができます。 

たとえば、一般的な DMA 対応の NIC を検討してください。 ストアには、このアプローチにまでの利点があります。

1. データ バッファーに割り当てられ、システムによって解放されます。 そのため、クライアント ドライバーは、メモリの有効期間管理の負担から解放されます。
2. システムにより、割り当て済みのデータ バッファーにあるクライアント ドライバーで宣言されている機能に基づく NIC ハードウェアの DMA の準備完了です。 次に、クライアント ドライバーだけにプログラムできるデータ バッファーとして、ハードウェアの追加の DMA マッピング操作を実行せず。
3. システムにローカル エンド ツー エンドのパフォーマンスだけではなくグローバルのエンド ツー エンドのパフォーマンスを最適化するために決定できるようには、バッファーのデータを割り当てるときに考慮上位層のアプリケーションのニーズを実行できます。

非 DMA capabile Nic などの USB ベースのネットワーク ドングルまたは他の高度/ソフトウェア Nic バッファー管理モデルが用意されています、クライアント ドライバーを完全にデータ バッファー管理のままにするオプション。 

## <a name="how-to-leverage-buffer-management"></a>バッファー管理を活用する方法

> [!IMPORTANT]
> ハードウェアが DMA サポートしている場合は、Rx、Tx 機能を設定する前に WDFDMAENABLER オブジェクトを作成する必要があります。 WDFDMAENABLER オブジェクトを構成するときに、 [ **WDF_DMA_ENABLER_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)構造体を設定することを確認、 **WdmDmaVersionOverride** メンバー**3** DMA バージョン 3 を指定します。

バッファー管理するオプトインするには、これらの手順に従います。

1. ネット アダプターを開始するときに、呼び出す前に[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)、ハードウェアのデータ バッファーの機能や制約を使用して通知システム、 [ **NET_ADAPTER_RX_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/ns-netadapter-_net_adapter_rx_capabilities)と[ **NET_ADAPTER_TX_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/ns-netadapter-_net_adapter_tx_capabilities)データは、Rx、Tx パスをそれぞれ構造体します。 
2. 初期化関数の 1 つを呼び出すことによって、2 つの機能の構造体を初期化します。 たとえば、DMA 対応の NIC のクライアント ドライバーは使用[ **NET_ADAPTER_TX_CAPABILITIES_INIT_FOR_DMA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_tx_capabilities_init_for_dma)と[ **NET_ADAPTER_RX_CAPABILITIES_INIT_SYSTEM_MANAGED** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_rx_capabilities_init_system_managed)そのハードウェア DMA capablities を宣言して、自身のためにデータ バッファーを完全に管理するシステムに指示します。
3. 初期化された送受信機能の構造に渡す、 [ **NetAdapterSetDatapathCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)メソッド。


## <a name="example"></a>例

次の例は、NIC は、クライアント ドライバー バッファー マネージャーの使用を開始する方法については、前のセクションに記載されている基本的な手順を示しています。 例は、そのデバイス コンテキストの領域に保存しておいた WDFDMAENABLER オブジェクトを以前に作成したので、テキサス州と Rx では、両方の DMA を使用します。 

送受信機能の構造体を初期化した後、例がそのフラグメント バッファーが、いくつかのヒントも設定されるに注意してください。 これらのヒントは、NetAdapterCx およびプロトコルのドライバーによってパフォーマンスを向上させるために使用できます。

エラー処理はわかりやすくするため省略してをいます。

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
