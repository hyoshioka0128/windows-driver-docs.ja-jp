---
title: Hyper-v 拡張可能スイッチのハイブリッド転送
description: このセクションでは、Hyper-v 拡張可能スイッチを使用したハイブリッド転送について説明します。
ms.assetid: 135CA734-1C92-4EEA-81DC-96A6A68ABBE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 919163be546e9ead02ae862bc2d9f040bf579799
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823922"
---
# <a name="hybrid-forwarding"></a>ハイブリッド転送


NDIS 6.40 (Windows Server 2012 R2 以降の Hyper-v 拡張可能スイッチアーキテクチャでは、拡張可能スイッチの Hyper-v ネットワーク仮想化 (HNV) コンポーネントによるハイブリッド転送と、拡張機能の転送がサポートされています。

**注**  このページは、[汎用ルーティングカプセル化 (Nvgre) タスクオフロードを使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)について理解していること、および[Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)を前提としています。

 

## <a name="nvgre-and-non-nvgre-packets"></a>NVGRE および NVGRE 以外のパケット


ハイブリッド転送環境では、次の2種類のパケットを使用して Hyper-v 拡張可能スイッチを入力し、そのままにします。 NVGRE パケットと非 NVGRE パケット:

-   NVGRE パケットのカプセル化された形式は、 [nvgre: ネットワーク仮想化で汎用ルーティングカプセル化インターネットドラフトを使用](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)して指定されます。 NVGRE パケットは、Hyper-v 拡張可能スイッチの HNV コンポーネントによって転送されます。
-   NVGRE 以外のパケットは、通常のネットワークパケットにすぎません。 非 NVGRE パケットは転送拡張機能によって転送されます (または、転送拡張機能がない場合は、拡張可能なスイッチ自体が存在します)。

## <a name="flow-of-nvgre-and-non-nvgre-packets-through-the-switch"></a>スイッチを介した NVGRE パケットと NVGRE 以外のパケットのフロー


受信データパスでは、拡張機能のキャプチャとフィルター処理の後、転送拡張機能の前に、パケットが NVGRE パケットの場合、拡張可能スイッチは NDIS\_スイッチに**NativeForwardingRequired**フラグを設定し[ **\_\_詳細\_NET\_\_BUFFER に転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)し、パケットの\_情報構造を一覧表示します。 この構造体は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の**NetBufferListInfo**メンバーに含まれています。

[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の**NetBufferListInfo**メンバーは、パケットの "帯域外 (OOB) データ" と呼ば**れることが**あります。  

 

パケットの OOB データに**NativeForwardingRequired**フラグが設定されている場合、パケットは nvgre パケットです。 設定されていない場合、パケットは NVGRE 以外のパケットです。

拡張機能では、NET\_BUFFER\_LIST を使用して、 **NativeForwardingRequired**フラグの値を確認するために[ **\_転送\_詳細マクロ\_切り替える**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)必要があります。

NVGRE パケットと NVGRE 以外のパケットは、次のように処理されます。

-   Hyper-v 拡張可能スイッチの HNV コンポーネントは、すべての NVGRE パケットを転送します (つまり、によって宛先テーブルが決定されます)。
-   HNV コンポーネントは、必要に応じて NVGRE カプセル化とカプセル化解除を実行します。
-   転送拡張機能は、NVGRE 以外のすべてのパケットを転送します。
-   転送拡張機能は NVGRE パケットを転送できませんが、宛先ポートの追加や除外、パケットの破棄など、フィルター拡張と同じフィルター処理操作を実行できます。
-   転送拡張機能がない場合、Hyper-v 拡張可能スイッチはすべてのパケットを転送します。

詳細については、「[拡張可能スイッチのデータパスを介したパケットフロー](packet-flow-through-the-extensible-switch-data-path.md)」を参照してください。

## <a name="support-for-third-party-network-virtualization"></a>サードパーティのネットワーク仮想化のサポート


**VirtualSubnetId**は、VM ネットワークアダプターポートで外部仮想サブネットとして構成できます。 この機能は、転送拡張機能を使用してサードパーティのネットワーク仮想化ソリューションを提供するために追加されました。 受信時には、Hyper-v 拡張可能スイッチは、これらのパケットの**NativeForwardingRequired**フラグを[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に設定しません。 転送拡張機能は、転送中に必要に応じてパケットヘッダーを変更できます。 変更されるパケットは複製され、その**ParentNetBufferList**ポインターが元の**NET\_BUFFER\_LIST**に設定されている必要があります。 (「[パケットトラフィックの複製](cloning-or-duplicating-packet-traffic.md)」を参照してください)。

## <a name="related-topics"></a>関連トピック


[拡張可能なスイッチの宛先ポートデータをパケットに追加する](adding-extensible-switch-destination-port-data-to-a-packet.md)

[パケットトラフィックの複製](cloning-or-duplicating-packet-traffic.md)

[拡張機能の転送](forwarding-extensions.md)

[拡張可能なスイッチのデータパスを介したパケットフロー](packet-flow-through-the-extensible-switch-data-path.md)

[**NET\_BUFFER\_LIST\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)

[**NDIS\_スイッチ\_転送\_詳細\_NET\_BUFFER\_LIST\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)

 

 






