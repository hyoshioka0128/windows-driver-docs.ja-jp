---
title: 物理ネットワーク アダプターへのパケットの転送
description: 物理ネットワーク アダプターへのパケットの転送
ms.assetid: 14A78DB2-6643-471D-97B9-4D8524EC3E73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a08b51133c84670f954e7c91914fc3c0284e587
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387299"
---
# <a name="forwarding-packets-to-physical-network-adapters"></a>物理ネットワーク アダプターへのパケットの転送


**注**  このページでは、情報と、次のページの図に精通していることを前提としています。
-   [転送拡張機能](forwarding-extensions.md)
-   [ハイブリッド転送](hybrid-forwarding.md)
-   [HYPER-V 拡張可能スイッチの拡張機能](hyper-v-extensible-switch-extensions.md)
-   [HYPER-V 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)
-   [プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)

 

このページでは、どの HYPER-V 拡張可能スイッチ転送拡張機能転送要求を送信できるパケットの基になる物理アダプターをについて説明します。 1 つまたは複数の物理ネットワーク アダプターは、拡張可能スイッチの外部ネットワーク アダプターにバインドできます。

たとえば、拡張可能スイッチの外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX 中間ドライバー自体は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドできます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。 拡張可能スイッチ チームの詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)します。

この構成では、拡張可能スイッチ拡張機能は拡張可能スイッチ チームのすべてのネットワーク アダプターに公開されます。 これにより、転送拡張機能が拡張可能スイッチのドライバー スタックを構成し、チーム内の個々 のネットワーク アダプターの使用を管理するの。 たとえば、拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 拡張機能と呼ばれるなど、*チーミング プロバイダー*します。 プロバイダーのチーミングの詳細については、次を参照してください。[プロバイダーの拡張機能のチーミング](teaming-provider-extensions.md)します。

転送拡張機能をインストールして、拡張可能スイッチ ドライバー スタックで有効にすると場合、は、パケットが、NVGRE パケットでない限り、拡張可能スイッチのイングレス データ パスを取得する各パケットの転送に関する決定を行う責任を負います。 (詳細については、NVGRE パケットは、次を参照してください[ハイブリッド転送](hybrid-forwarding.md)。)。この情報に基づいて意思決定を転送、拡張機能を追加できます宛先ポートのパケットのアウト オブ バンド (OOB) データに[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 パケットが完了したらそのトラバーサル拡張可能スイッチのインターフェイスは、拡張可能スイッチ データ パスの指定の宛先ポートへのパケットします。

**注**  転送拡張機能がインストールされていないか、有効になっている場合、拡張可能なスイッチ自体は、転送パケットの受信データのパスから取得を決定します。 スイッチのパケットの OOB データに宛先ポートを追加する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)拡張可能スイッチのエグレス データ パケットを転送する前に構造体パス。

 

ときに、転送拡張機能の[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)関数が呼び出されると、 *NetBufferList*パラメーターのリンクリストへのポインターを格納する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 各構造体には、受信データのパスから取得したパケットを指定します。 内の各パケットの OOB データ**NET\_バッファー\_一覧**構造の場合は、宛先ポートに含まれるため、データ、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 拡張機能を取得、 **NDIS\_スイッチ\_転送\_先\_配列**構造とその要素を呼び出して[ *GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)します。

**注**  パフォーマンスを向上させるには、転送拡張機能を呼び出すことができます、 [ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数の代わりに[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)へのポインターを取得する、 [ **NDIS\_スイッチ\_転送\_先\_配列** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 拡張機能は宛先ポートのパケットの OOB データに追加の配列の要素が必要であると判断した場合、します。 詳細については、次を参照してください。[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)します。

 

内の各要素、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)配列が宛先ポートを定義し、として書式設定[**NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体。 この構造体には、次のメンバーが含まれています。

-   **PortId**メンバーには、拡張可能スイッチに接続先ポートを指定する値が含まれています。

-   **NicIndex**メンバーで指定された拡張可能スイッチ ポートに接続されているネットワーク アダプターのインデックスを指定する、 **PortId**メンバー。

    これらのインデックス値の詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。

転送拡張機能は、外部ネットワーク アダプターに接続されている接続先ポートを追加する場合、拡張機能は、基になる物理ネットワーク アダプターのインデックスを指定できます。 など、拡張機能は、over、拡張可能スイッチ チームのサポートの LBFO チーミング プロバイダーとして動作する可能性があります。 これにより、チームの別のアダプターに送信要求を転送することによって、トラフィックのオーバーヘッドのバランスを取る拡張機能です。

転送拡張機能は、それを追加または変更時にこれらのガイドラインに従う必要があります、 [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)転送を送信する構造体基になる物理ネットワーク アダプターへの要求:

-   場合、 **PortId**メンバーは、外部のネットワーク アダプターに拡張可能スイッチ ポートが接続されている、拡張機能を設定する必要がありますを指定します、 **NicIndex**インデックス値は次のいずれかにメンバー。

    -   拡張機能を設定する必要があります 1 つの物理ネットワーク アダプターは外部ネットワーク アダプターにバインドする場合のみ、 **NicIndex**メンバー **NDIS\_スイッチ\_既定\_NIC\_インデックス**またはいずれか。

    -   複数の物理ネットワーク アダプターは、外部ネットワーク アダプターにバインドする場合、拡張機能を設定する必要があります、 **NicIndex**メンバーを拡張可能スイッチ チームの移行先ネットワーク アダプターの 0 以外のインデックス値。

    **注**  場合、 **PortId**を外部ネットワーク アダプターの拡張可能スイッチ ポートが接続されている、拡張機能を設定する必要があります、メンバーが指定されていない、 **NicIndex**メンバー**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

     

-   呼び出す必要がありますが、拡張機能がすべて、パケットの宛先ポートの追加後[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)イングレス データ パス上のパケットを転送するようにします。

パケットを宛先ポートを追加する方法の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ ポートのパケットの転送](forwarding-packets-to-hyper-v-extensible-switch-ports.md)します。

出口データ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)します。

 

 





