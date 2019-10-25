---
title: ネットワーク インターフェイス カードのサポート
description: ネットワーク インターフェイス カードのサポート
ms.assetid: de673a37-3870-4995-b4f1-647b502e0773
keywords:
- ミニポートドライバー WDK ネットワーク、NIC サポート
- NDIS ミニポートドライバー WDK、NIC サポート
- Nic WDK ネットワーク、種類
- ネットワークインターフェイスカード WDK ネットワーク、種類
- バスマスタ DMA Nic WDK ネットワーク
- 非バスマスタ DMA Nic WDK ネットワーク
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3cc696b3e062f3c69b60830fb7cea8f3b5a05181
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827226"
---
# <a name="network-interface-card-support"></a>ネットワーク インターフェイス カードのサポート

このトピックでは、NDIS ミニポートドライバーが管理できるネットワークインターフェイスカード (Nic) の種類、およびさまざまな種類の Nic がドライバーによるネットワークデータの転送方法に与える影響について説明します。

## <a name="reporting-a-nics-medium-type-to-ndis"></a>NIC のメディアの種類を NDIS に報告する

NIC のメディアの種類を報告するために、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造へのポインターを、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数。 ミニポートドライバーは、初期化中に[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数から**NdisMSetMiniportAttributes**を呼び出します。 ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造の登録属性を設定してから、その他の設定を行う前に、 *miniportattributes*属性を設定する必要があります。アトリビュート. *Miniportattributes*属性の設定は必須です。 このドライバーは、 *Miniportattributes*属性を設定するときに、 **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**構造体の**MediaType**メンバーを適切なメディアの種類に設定します。

1つの NDIS プロトコルドライバーが[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)を呼び出して、指定されたミニポートアダプターにバインドすると、実行可能な中規模の種類の一覧が提供されます。 NDIS は、ミニポートドライバーとプロトコルドライバーからの情報を使用してバインドを設定します。 このバインディングは、ネットワークデータをドライバースタックの上下に転送するためのパスを提供します。

## <a name="physical-nics"></a>物理 Nic

ミニポートドライバーがミニポートアダプターを初期化してネットワークデータを送受信するために完了する手順は、次のように、物理デバイスの機能によって異なります。

- NDIS-WDM Nic

    USB ベースの Nic などの NDIS-WDM Nic では、ミニポートドライバーが DMA を使用してメモリを管理する方法は NDIS には関係なく、表示されません。

- バスマスタ DMA Nic

    これらの Nic は、ホストの CPU を使用せずに、ネットワークとホストのメモリ間のデータ転送を管理するオンボードの DMA コントローラーを介してホストメモリに直接アクセスできます。

    送信するために、ミニポートドライバーは、送信バッファーをマップするように NIC を設定します。 その後、ミニポートドライバーによって、デバイスはこのメモリからの転送を開始します。 NIC DMA コントローラーは、共有システムメモリからネットワークにデータを転送し、送信が完了すると CPU を中断します。 受信するために、DMA コントローラーは、ホストに割り込みを通知する前に、受信データをホストメモリに転送します。

    通常、バスマスタ DMA NIC には、ミニポートドライバーがシステムメモリ内のバッファーのセットにマップされるオンボードリングバッファーがあります。 通常、複数のパケットを効率的に処理するように NIC をプログラミングできます。 通常、このような NIC を管理するミニポートドライバーは複数のパケットの送受信をサポートしているため、NIC は複数のパケットを効率的に処理し、その結果、i/o スループットを向上させることができます。

- 非バスマスター DMA Nic

    現時点では、非バスマスター DMA Nic には次のものが含まれています。

    -   システム DMA Nic

        このような NIC を管理するミニポートドライバーは、システム DMA コントローラーを使用して、ネットワークとの間でのパケットデータの転送を管理します。 データの転送には、ホスト CPU の連携が必要です。

## <a name="virtual-nics-and-miniports"></a>仮想 Nic とミニポート

仮想マシンでは、NDIS ミニポートドライバーは、ソフトウェアのみのリソースを仮想ミニポートとして管理するか、ハードウェアリソースを表す仮想 NIC を管理できます。 次の表では、仮想ミニポートと仮想 NIC の違いについて説明します。

|   | 仮想ミニポート | 仮想 NIC |
| --- | --- | --- |
| 定義 | ソフトウェアで列挙された PnP デバイスにマップされる NDIS ミニポートドライバー。 | ホスト OS ハイパーバイザーによって管理される NIC。 ハイパーバイザーによって、仮想マシンはハードウェアがいくつかあると考えられますが、実際には物理環境には存在しません。 |
| 割り込みあり | 必須ではない | [はい] |
| DMA を使用可能 | 必須ではない | [はい] |
| 作成または破棄する方法... | ゲスト OS | ホスト OS |
| ゲスト VM の外部に接続可能 | 必須ではない | [はい] |
