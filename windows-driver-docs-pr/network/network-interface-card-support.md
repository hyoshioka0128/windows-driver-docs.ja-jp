---
title: ネットワーク インターフェイス カードのサポート
description: ネットワーク インターフェイス カードのサポート
ms.assetid: de673a37-3870-4995-b4f1-647b502e0773
keywords:
- ミニポート ドライバー WDK ネットワーク、NIC のサポート
- NDIS ミニポート ドライバー WDK には、NIC をサポートします。
- Nic WDK ネットワー キング、種類
- ネットワーク インターフェイス カード WDK ネットワークの種類
- バス マスター DMA Nic WDK ネットワーク
- バス マスター以外の DMA Nic WDK ネットワーク
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b2aa3ec1d96a52b8d4f3b66d2b1a2b961b30ceb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386323"
---
# <a name="network-interface-card-support"></a>ネットワーク インターフェイス カードのサポート

このトピックでは、NDIS ミニポート ドライバーを管理するにもさまざまな種類の Nic のドライバーは、ネットワーク データを転送する方法に影響を与える方法、ネットワーク インターフェイス カード (Nic) の型について説明します。

## <a name="reporting-a-nics-medium-type-to-ndis"></a>NDIS に NIC のメディアの種類を報告します。

NIC のメディアの種類を報告するミニポート ドライバーがへのポインターを渡す、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体、 *MiniportAttributes*のパラメーター、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。 ミニポート ドライバーは呼び出し**NdisMSetMiniportAttributes**からその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)初期化中に機能します。 ミニポート ドライバーを設定する必要があります、 *MiniportAttributes*属性で登録属性を設定した後、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体し、その他の属性を設定する前にします。 設定、 *MiniportAttributes*属性は必須です。 ドライバーのセット、 **MediaType**のメンバー、 **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**構造体を設定するときに、適切なメディアの種類を*MiniportAttributes*属性。

上位の NDIS プロトコル ドライバーを呼び出すと[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)指定ミニポート アダプターにバインドする、動作できるメディアの種類の一覧を提供します。 NDIS では、ミニポート ドライバーとプロトコル ドライバーからの情報を使用して、バインドを設定します。 このバインディングでは、ドライバー スタックとネットワークのデータを転送するためのパスを提供します。

## <a name="physical-nics"></a>物理 Nic

ミニポート アダプターを初期化して、ネットワーク データを送受信するミニポート ドライバーが完了する手順は、次のように、物理デバイスの機能に依存できます。

- NDIS WDM Nic

    USB ベースの Nic など、NDIS WDM Nic を持つミニポート ドライバーは、DMA を使用してメモリを管理する方法は NDIS には必要ありませんし、それには表示されません。

- バス マスター DMA Nic

    これらの Nic は、ホストの CPU を使用せず、ネットワークとホストのメモリ間のデータ転送を管理するオンボード DMA コント ローラーで、ホストのメモリを直接アクセスできます。

    ミニポート ドライバーはを送信するには、送信バッファーをマップする NIC を設定します。 ミニポート ドライバーは、このメモリからその転送を開始するデバイスを引き起こします。 NIC の DMA コント ローラーは、送信が完了すると、ネットワークと CPU の割り込みの上に共有のシステム メモリからデータを転送します。 受信するには、DMA コント ローラーは、ホストのメモリに割り込みをホストに通知する前に受信データを転送します。

    バス マスター DMA NIC には、通常、ミニポート ドライバーは、一連のシステム メモリにバッファーにマップされるオンボードのリング バッファーがあります。 通常、いくつかのパケットを効率的に処理するために、NIC をプログラミングできます。 このような NIC を管理するミニポート ドライバー通常サポート multipacket は送受信ため、NIC がいくつかのパケットを効率的に処理し、I/O スループットが向上します。

- Nonbusmaster DMA Nic

    現時点では、nonbusmaster DMA Nic は、次に示します。

    -   システムの DMA Nic

        このような NIC を管理するミニポート ドライバーでは、ネットワークとの間のパケット データの転送を管理するのにシステムの DMA コント ローラーを使用します。 データの転送には、ホストの CPU の協力が必要です。

## <a name="virtual-nics-and-miniports"></a>仮想 Nic とミニポート

仮想マシンでは、NDIS ミニポート ドライバーが仮想のミニポートとしていずれかのソフトウェア専用のリソースを管理できるまたはハードウェア リソースを表す仮想 NIC を管理することができます。 次の表に、仮想ミニポートと仮想 NIC の違い

|   | 仮想ミニポート | 仮想 NIC |
| --- | --- | --- |
| 定義 | NDIS ミニポート ドライバーのソフトウェア列挙の PnP デバイスにマップされます。 | NIC は、OS のハイパーバイザー ホストによって管理されます。 ハイパーバイザーは、仮想マシン、ハードウェアの一部が、実際には、現実の世界では、このようなハードウェアが存在しないことを検討します。 |
| 割り込みをが | X | 〇 |
| DMA を使用できます。 | X | 〇 |
| 作成または破棄しています. | ゲスト OS | ホスト OS |
| ゲスト VM の外部にアクセスできます。 | X | 〇 |
