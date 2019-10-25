---
title: パケットへの拡張可能スイッチ宛先ポート データの追加
description: パケットへの拡張可能スイッチ宛先ポート データの追加
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6dac07f83f234a043ca75a843c0a5134e35678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838239"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>パケットへの拡張可能スイッチ宛先ポート データの追加


このトピックでは、Hyper-v 拡張スイッチ転送拡張機能が、1つまたは複数の宛先ポートへのパケットの配信を指定する方法について説明します。 これらの拡張機能は、拡張可能スイッチの外部ネットワークアダプターにバインドされている個々の物理ネットワークアダプターにパケットを転送することもできます。

**メモ** 転送拡張機能またはスイッチ自体だけが、拡張可能なスイッチポートまたは個々のネットワークアダプターにパケットを転送できます。



次の図は、NDIS 6.40 (Windows Server 2012 R2) 以降の拡張可能なスイッチドライバースタックを介したパケットトラフィックのデータパスを示しています。 どちらの図も、拡張可能なスイッチポートに接続されているネットワークアダプターとの間のパケットトラフィックのデータパスを示しています。

![ndis 6.40 用に更新された拡張スイッチポートに接続されているネットワークアダプターとの間のパケットトラフィックのデータパスを示すフローチャート](images/vswitchteam2-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能なスイッチドライバースタックを介したパケットトラフィックのデータパスを示しています。

![拡張可能なスイッチポートに接続されているネットワークアダプターとの間のパケットトラフィックのデータパスを示すフローチャート](images/vswitchteam2.png)

拡張可能な各スイッチの宛先ポートは、ndis\_スイッチで指定されています。この場合、Ndis\_スイッチ内の[ **\_port\_destination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)要素によって\_転送[**先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造に転送されます。 この配列は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の帯域外 (OOB) 転送コンテキストに含まれています。 このコンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

拡張可能なスイッチドライバースタックで転送拡張機能がバインドされ、有効になっている場合は、パケットが NVGRE パケットでない限り、拡張可能スイッチの受信データパスから取得したすべてのパケットの宛先ポートを決定します。 このデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパスの概要](overview-of-the-hyper-v-extensible-switch-data-path.md)」を参照してください。 NVGRE パケットの詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

**メモ** 転送拡張機能がドライバースタックでバインドされていない場合、または有効になっていない場合は、拡張可能スイッチによって、受信データパスから取得するパケットの宛先ポートが決まります。



転送拡張機能は、受信データパスで取得したパケットの宛先ポートを決定するときに、次のガイドラインに従う必要があります。

-   拡張機能では、ndis\_スイッチ内の[**ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造を初期化する必要があります。この\_\_とき\_[**宛先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造を宛先ポートに転送\_ます。参照.

    宛先ポートが外部ネットワークアダプターに接続されていない場合、拡張機能では、 [**ndis\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造の**NicIndex**メンバーを ndis\_スイッチに設定する必要があります **\_既定値\_NIC\_インデックス**です。

    宛先ポートが拡張可能スイッチの外部ネットワークアダプターに接続されている場合、この拡張機能では、送信要求の転送先となる、基になる物理ネットワークアダプターのインデックスを指定できます。 拡張機能は、外部ネットワークアダプターにバインドされている宛先ネットワークアダプターの NIC\_インデックス値\_、 **NicIndex**メンバーを0以外の NDIS\_スイッチに設定することによってこれを行います。

    詳細については、「[物理ネットワークアダプターへのパケットの転送](forwarding-packets-to-physical-network-adapters.md)」を参照してください。

-   拡張機能では、アクティブなネットワークアダプター接続があるポートに対してのみ、パケットの OOB データに宛先ポートを追加する必要があります。 拡張機能が[OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)要求を転送した場合、切断されたネットワークアダプターに関連付けられている宛先ポートを追加することはできません。

-   パフォーマンスを向上させるには、拡張機能で、パケット配信に有効なポートの宛先だけを追加する必要があります。 この場合、拡張機能では、宛先ポートの[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造の**ISEXCLUDED**メンバーを FALSE に設定する必要があります。

-   ポートに送信される前に 802.1 Q 仮想ローカルエリアネットワーク (VLAN) のデータをパケットで保持するために、拡張機能は**PreserveVLAN**メンバーを TRUE に設定します。

    パケット内の 802.1 Q 仮想ローカルエリアネットワーク (VLAN) データをポートに配信する前に削除するには、拡張機能によって**PreserveVLAN**メンバーが FALSE に設定されます。

-   ポートに送信される前に 802.1 Q 優先順位データをパケットで保持するために、拡張機能は**PreservePriority**メンバーを TRUE に設定します。

    パケット内の 802.1 Q 優先度データをポートに配信する前に削除するには、拡張機能によって**PreservePriority**メンバーが FALSE に設定されます。

-   転送拡張機能によってパケットに複数の宛先ポートが追加される場合は、次の手順に従う必要があります。

    1.  拡張機能は、最初にパケットの NDIS\_スイッチにアクセスし\_Net\_BUFFER\_list\_\_を使用して[ **\_詳細 net\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info) buffer\_list\_を転送します。 [ **\_\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロを転送します。 拡張機能は、 **numavailable** destination メンバーを読み取り、宛先ポートアレイで使用可能な未使用の宛先ポート要素の数を確認します。 拡張機能が配列で使用可能なよりも多くの宛先ポートを必要とする場合は、 [*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数を呼び出して、配列内の追加の宛先ポートに領域を割り当てる必要があります。

        拡張機能が[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)を呼び出すと、 *numberofnewdestinations*パラメーターが、パケットに追加される新しい宛先ポートの数に設定されます。

        また、この拡張機能は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体へのポインターに、 *NetBufferLists*パラメーターを設定します。

        **メモ** 配列に使用できる宛先ポートがある場合、拡張機能は[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)を呼び出すことはできません。

    2.  [*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数が正常に復帰した場合は、追加の宛先ポートが NDIS\_スイッチ内のコピー先配列の末尾に追加されて[ **\_転送先\_配列に転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)ます。データ. この構造体へのポインターは、*変換先*パラメーターで返されます。

        **メモ** [*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数が、要求された数の宛先ポートを割り当てることができない場合、NDIS\_STATUS\_リソースを返します。

    3.  拡張機能は、[**ターゲット\_配列構造の\_転送\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)内の新しい宛先ポート要素を指定します。 拡張機能は、新しい宛先ポートを[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体として初期化します。

        拡張機能は、 **numdestinations**オフセットを開始位置として、新しい宛先ポートを配列に初期化します。 **NUMDESTINATIONS**は、[**ターゲット\_配列構造\_転送\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)のメンバーです。

    4.  拡張機能が宛先ポート要素の追加または変更を完了したら、 [*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)を呼び出して変更をコミットする必要があります。

-   拡張機能によってパケットの宛先ポートが1つ追加された場合は、次の手順に従う必要があります。

    1.  拡張機能によって、拡張機能によって割り当てられた[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造で、パケットの宛先ポート情報が初期化されます。

    2.  拡張機能は、 [*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)を呼び出して、変更をパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造にコミットします。 拡張機能は、*ターゲット*パラメーターで、 [**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体のアドレスを渡します。

        **メモ** 拡張機能では[*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)関数を呼び出して、宛先ポートが1つだけのパケットに変更をコミットすることはできません。

-   転送拡張機能が[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)または[*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)を呼び出して、宛先ポートの変更をコミットすると、拡張可能なスイッチインターフェイスは、以下の拡張可能なスイッチポートを削除しません。NDIS\_スイッチの要素で指定され[ **\_転送先\_配列構造体\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)します。 パケットの送信または受信操作が完了したら、必要に応じて、インターフェイスでポートを自由に削除できます。

    **メモ** 転送拡張機能によって宛先ポートの変更が転送コンテキストにコミットされた後、宛先ポートを削除することはできず、宛先ポートの NDIS\_の**IsExcluded**メンバのみが\_ポートを切り替えることができ[ **\_ターゲット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造は変更できます。 詳細については、「[拡張可能スイッチの接続先ポートへのパケット配信の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)」を参照してください。

-   転送拡張機能は、Oid のオブジェクト識別子 (OID) セット要求の処理を同期する必要があります。 [\_スイッチ\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)は、切断されたネットワークアダプターの宛先ポートを追加するコードとの接続を解除\_ます。

    転送拡張機能の[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)が[OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)要求に対して呼び出された場合、拡張機能は次のいずれかの操作を実行できます。

    -   この OID 要求を転送するために拡張機能が[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出した場合、切断されたネットワークアダプターのポートをパケットの宛先ポートとして指定することはできません。

        **メモ** パケットの宛先ポートが切断されたネットワークアダプターと同じである場合、拡張機能はパケットを削除する必要があります。

    -   拡張機能は、要求を非同期的に完了するために、NDIS\_STATUS\_PENDING を返すことができます。 これにより、拡張機能は、切断されたネットワークアダプターを使用するポートを、パケットの宛先ポートとして追加できます。 これにより、拡張機能が[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)または[*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)を呼び出し、パケットへの宛先ポートの追加を完了することもできます。

        拡張機能は、パケットが破棄される前にポートに転送する必要があるパケットに対して、このような処理を行うことができます。

        **メモ** 拡張機能によって、NDIS\_STATUS\_PENDING が返された場合、参照可能な[*Chport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)を呼び出して、切断されたネットワークアダプターでポートの参照カウンターをインクリメントすることもできます。 ただし、拡張機能は、 [*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)を呼び出してポートの参照カウンターをデクリメントするまで OID 要求を転送できません。



-   宛先ポートの数が0の場合、転送拡張機能は[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)を呼び出してパケットを削除する必要があります。 拡張機能は、 [*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)を呼び出して、ドロップされたパケットについて拡張可能なスイッチインターフェイスに通知する必要もあります。

    **メモ** 転送拡張機能が、受信データパスからの複数のパケットについて、 [**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストを取得した場合は、破棄されたパケットの個別のリストを作成する必要があります。 これにより、拡張機能は[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)と[*ReportFilteredNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)を1回だけ呼び出すことができます。



-   宛先ポートの数が0より大きい場合、転送拡張機能は[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出して、拡張可能スイッチのミニポートエッジにパケットを受信データパス経由で転送する必要があります。

    **メモ** 転送拡張機能が、受信データパスからの複数のパケットについて、 [**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストを取得した場合、転送されたパケットの別のリストを作成する必要があります。 これにより、拡張機能は[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を1回だけ呼び出して、パケットの一覧を転送できます。 さらに、同じ宛先ポートを持つパケットを転送するために、拡張機能は個別のリストを保持する必要があります。 詳細については、「 [Hyper-v 拡張可能スイッチの送信フラグと受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)」を参照してください。