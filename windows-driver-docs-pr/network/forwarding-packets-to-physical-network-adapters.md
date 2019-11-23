---
title: 物理ネットワーク アダプターへのパケットの転送
description: 物理ネットワーク アダプターへのパケットの転送
ms.assetid: 14A78DB2-6643-471D-97B9-4D8524EC3E73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e67a355a442b82e39cb915aeca50a4ac55eb5d8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842123"
---
# <a name="forwarding-packets-to-physical-network-adapters"></a>物理ネットワーク アダプターへのパケットの転送


**注**  このページでは、次のページの情報と図について理解していることを前提としています。
-   [拡張機能の転送](forwarding-extensions.md)
-   [ハイブリッド転送](hybrid-forwarding.md)
-   [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)
-   [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)
-   [チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)

 

このページでは、Hyper-v 拡張スイッチ転送拡張機能がパケットの送信要求を基になる物理アダプターに転送する方法について説明します。 1つまたは複数の物理ネットワークアダプターを拡張スイッチの外部ネットワークアダプターにバインドできます。

たとえば、拡張可能スイッチの外部ネットワークアダプターは、NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドできます。 MUX 中間ドライバー自体は、ホスト上の1つまたは複数の物理ネットワークのチームにバインドできます。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。 拡張可能なスイッチチームの詳細については、「[物理ネットワークアダプターの構成の種類](types-of-physical-network-adapter-configurations.md)」を参照してください。

この構成では、拡張可能なスイッチ拡張機能は、拡張可能なスイッチチームのすべてのネットワークアダプターに公開されます。 これにより、拡張可能なスイッチドライバースタックで転送拡張機能を使用して、チーム内の個々のネットワークアダプターの構成と使用を管理できます。 たとえば、拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 たとえば、拡張機能は*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

拡張可能なスイッチドライバースタックに転送拡張機能がインストールされ、有効になっている場合は、パケットが NVGRE パケットでない限り、拡張スイッチの受信データパスで取得する各パケットについて、転送の決定を行う必要があります。 (NVGRE パケットの詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください)。これらの転送の決定に基づいて、拡張機能はパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の帯域外 (OOB) データに宛先ポートを追加できます。 パケットが拡張可能なスイッチのデータパスのトラバーサルを完了すると、拡張可能なスイッチインターフェイスは、指定された宛先ポートにパケットを配信します。

**注**  転送拡張機能がインストールされていない場合、または有効になっていない場合は、拡張可能なスイッチ自体によって、受信データパスから取得したパケットの転送の決定が行われます。 スイッチは、拡張可能なスイッチの送信データパスにパケットを転送する前に、パケットの[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データに宛先ポートを追加します。

 

転送拡張機能の[*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数が呼び出されると、 *NetBufferList*パラメーターには、 [**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストへのポインターが含まれます。 これらの各構造体は、受信データパスから取得したパケットを指定します。 各パケットの**NET\_BUFFER\_LIST**構造体の OOB データ内では、宛先ポートのデータが NDIS\_\_スイッチに格納され、[**転送先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造\_転送されます。 拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)を呼び出すことによって\_宛先\_配列構造とその要素を**転送\_、NDIS\_スイッチ**を取得します。

**注**  パフォーマンスを向上させるために、転送拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)の代わりに[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数を呼び出して、NDIS\_スイッチへのポインターを取得し[ **\_\_送信先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造を転送できます。 この拡張機能は、パケットの OOB データに追加の配列要素が必要であると判断した場合に、これを行います。 詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

 

[**Ndis\_スイッチ\_転送\_宛先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)配列の各要素は、宛先ポートを定義し、 [**ndis\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造としてフォーマットされます。 この構造体には、次のメンバーが含まれます。

-   **ポート id**メンバーには、拡張可能スイッチの宛先ポートを指定する値が含まれています。

-   **NicIndex**メンバーは、**ポート id**メンバーによって指定された拡張可能なスイッチポートに接続されているネットワークアダプターのインデックスを指定します。

    これらのインデックス値の詳細については、「[ネットワークアダプターのインデックス値](network-adapter-index-values.md)」を参照してください。

転送拡張機能によって、外部ネットワークアダプターに接続されている宛先ポートが追加された場合、拡張機能は、基になる物理ネットワークアダプターのインデックスを指定できます。 たとえば、拡張機能は、拡張可能なスイッチチームで LBFO をサポートするためのチーミングプロバイダーとして動作する可能性があります。 これにより、この拡張機能は、送信要求をチームのさまざまなアダプターに転送することによって、トラフィックのオーバーヘッドを分散させることができます。

転送拡張機能は、基になる物理ネットワークアダプターに送信要求を転送するために、 [**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造を追加または変更するときに、次のガイドラインに従う必要があります。

-   **ポート id**メンバーが、外部ネットワークアダプターが接続されている拡張可能なスイッチポートを指定する場合、拡張機能は**NicIndex**メンバーを次のいずれかのインデックス値に設定する必要があります。

    -   外部ネットワークアダプターにバインドされている物理ネットワークアダプターが1つのみの場合、拡張機能では**NicIndex**メンバーを**NDIS\_スイッチ\_既定の\_NIC\_インデックス**または1に設定する必要があります。

    -   複数の物理ネットワークアダプターが外部ネットワークアダプターにバインドされている場合、拡張機能は**NicIndex**メンバーを拡張可能なスイッチチームの宛先ネットワークアダプターの0以外のインデックス値に設定する必要があります。

    **注**  外部ネットワークアダプターが接続されている拡張可能なスイッチポートを**ポート id**メンバーが指定していない場合、拡張機能は**NICINDEX**メンバーを**NDIS\_スイッチ\_既定\_NIC\_インデックス**に設定する必要があります。

     

-   拡張機能によってパケットの宛先ポートがすべて追加されたら、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出してパケットを受信データパスに転送する必要があります。

宛先ポートをパケットに追加する方法の詳細については、「 [Hyper-v 拡張可能スイッチポートへのパケットの転送](forwarding-packets-to-hyper-v-extensible-switch-ports.md)」を参照してください。

送信データパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 





