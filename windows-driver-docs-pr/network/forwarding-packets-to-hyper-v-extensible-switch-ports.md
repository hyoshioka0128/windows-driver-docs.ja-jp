---
title: Hyper-V 拡張可能スイッチ ポートへのパケットの転送
description: Hyper-V 拡張可能スイッチ ポートへのパケットの転送
ms.assetid: C8DA9064-21EE-45F4-BE6D-D24851C5480B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e0be0155f20489369a10a0b472a84f586d41eba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839647"
---
# <a name="forwarding-packets-to-hyper-v-extensible-switch-ports"></a>Hyper-V 拡張可能スイッチ ポートへのパケットの転送


このページでは、Hyper-v 拡張可能スイッチ転送拡張機能が1つまたは複数のポートにパケットを転送する方法について説明します。 この種類の拡張機能では、拡張可能スイッチの外部ネットワークアダプターに接続されている個々のネットワークアダプターにパケットを転送することもできます。

**注**  拡張可能なスイッチ転送拡張機能または拡張可能なスイッチ自体だけが拡張可能なスイッチポートにパケットを転送できます。

 

**注**  このページでは、 [Hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。

 

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。 拡張機能の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)」を参照してください。

 

拡張可能なスイッチドライバースタックに転送拡張機能がインストールされ、有効になっている場合は、拡張スイッチの受信データパスで取得する各パケットについて、転送の決定を行う必要があります。 これらの転送の決定に基づいて、拡張機能はパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の帯域外 (OOB) データの宛先ポート配列に宛先ポートを追加します。 パケットが拡張可能なスイッチのデータパスのトラバーサルを完了すると、拡張可能なスイッチインターフェイスは、指定された宛先ポートにパケットを配信します。

**注**  転送拡張機能がインストールされていない場合、または有効になっていない場合は、拡張可能スイッチによって、受信データパスから取得したパケットの転送の決定が行われます。 スイッチは、拡張可能なスイッチの送信データパスにパケットを転送する前に、パケットの[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データに宛先ポートを追加します。

 

**注**  パケットが nvgre パケットの場合、転送拡張機能は宛先ポートを宛先ポート配列に追加できます。 ただし、拡張可能スイッチの Hyper-v ネットワーク仮想化 (HNV) コンポーネントは、宛先ポートを特定してパケットを転送する役割を担います。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

 

転送拡張機能は、受信データパスから取得したパケットにのみ、ポートの宛先を追加できます。 パケットが送信データパスの上位に転送されると、フィルターおよび転送拡張機能は、拡張可能なスイッチポートへのパケット配信を除外できます。 詳細については、「[拡張可能スイッチの接続先ポートへのパケット配信の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)」を参照してください。

パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データ内では、宛先ポートのデータは NDIS\_\_スイッチに格納され、[**転送先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造\_転送されます。 配列の各要素は宛先ポートを定義し、 [**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体としてフォーマットされます。

転送拡張機能は、次の Hyper-v 拡張可能スイッチハンドラー関数を呼び出して、宛先\_配列の構造と、その Ndis\_スイッチ\_ポート[ **\_転送\_、ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)を管理できます。 [**コピー先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)の要素\_:

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
この関数は、送信先ポートを NDIS\_スイッチに1つ追加し\_パケットの OOB データ内の[ **\_宛先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造を転送します。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
この関数は、パケットの OOB データ内の[ **\_宛先\_配列構造を転送\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)へのポインターを返します。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
この関数は、宛先ポートの要素を NDIS\_スイッチに追加して、パケットの OOB データの[ **\_配列構造を転送\_\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)します。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
この関数は、パケットの宛先ポートを追加または除外するために拡張機能によって行われた変更をコミットします。 これらの変更は、パケットの OOB データ内の[ **\_宛先\_配列構造の転送\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)にコミットされます。

転送拡張機能の[*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数が呼び出されると、 *NetBufferList*パラメーターには、 [**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストへのポインターが含まれます。 これらの各構造体は、受信データパスから取得したパケットを指定します。

この一覧の各[**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体では、次の手順に従って、転送拡張機能によってパケットの宛先ポートが追加されます。

1.  拡張機能は、さまざまな種類の条件に基づいて、パケットの転送に関する決定を行います。 これらの条件には、次のものがあります。

    -   パケットの発信元ポートとネットワークアダプター接続に基づくポリシーの条件。 転送拡張機能は、 [**NET\_BUFFER\_LIST\_スイッチ\_転送\_DETAIL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロを使用してこの情報を取得します。

    -   パケットのペイロードデータに基づく拡張可能なスイッチポートのポリシー条件。 たとえば、拡張可能なスイッチポートのポリシーには、IP version 4 (IPv4) パケットのみの配信を許可するフィルターを含めることができます。

    **注**  パケットが nvgre パケットの場合、拡張可能スイッチの hnv コンポーネントはパケットの転送を行います。 ただし、転送拡張機能では、受信パスと送信パスに独自のポリシー条件を適用できます。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

     

2.  拡張機能によって、パケットを1つ以上の拡張可能なスイッチポートに転送できることが決定された場合は、パケットの OOB データに宛先ポートを追加する必要があります。 この手順の詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

    **注**  パケットが nvgre パケットの場合、転送拡張機能は宛先ポートを追加する必要はありません。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

     

3.  拡張機能によって、パケットを拡張可能なスイッチポートに転送できないと判断された場合は、パケットを削除する必要があります。

    パケットが NVGRE パケットである場合は、これが当てはまる  ではない**ことに注意**してください。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

     

4.  拡張機能によってパケットの宛先ポートが1つ以上追加されている場合は、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出して、送信データパスにパケットを転送する必要があります。

    **注**  パケットが nvgre パケットの場合、拡張可能スイッチの hnv コンポーネントはパケットの転送を行います。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

     

拡張可能なスイッチの受信と送信のデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 





