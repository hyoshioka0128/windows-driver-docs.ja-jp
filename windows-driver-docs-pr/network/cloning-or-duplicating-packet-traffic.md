---
title: パケット トラフィックの複製
description: パケット トラフィックの複製
ms.assetid: 6BAE348D-B5BA-4B74-8D9B-79B146427D8C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab4008cac345e997d8d50d6b8fc7619c78e358d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835163"
---
# <a name="cloning-packet-traffic"></a>パケット トラフィックの複製


このトピックでは、Hyper-v 拡張可能スイッチ拡張機能がパケットを複製または複製し、拡張可能なスイッチのデータパスに挿入する方法について説明します。 パケットの複製の詳細については、「複製された[NET\_BUFFER\_LIST 構造体](cloned-net-buffer-list-structures.md)」を参照してください。

**メモ** このページでは、 [hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。

**メモ** 拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは*拡張可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。 拡張機能の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)」を参照してください。

拡張可能なスイッチのフィルター処理と転送拡張機能は、次のガイドラインに従って、複製されたパケットを拡張可能なスイッチの受信または送信データパスに挿入できます。

-   拡張機能は、まず、複製されたパケットに対して、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を割り当てる必要があります。 その後、拡張機能は、パケットデータを元のパケットから複製されたパケットにコピーする必要があります。 パケットを複製する方法の詳細については、「 [DERIVED NET\_BUFFER\_LIST 構造体](derived-net-buffer-list-structures.md)」を参照してください。

-   拡張機能によって、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体が割り当てられた後、 [*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) handler 関数を呼び出して、パケットの拡張可能なスイッチ転送コンテキストを割り当てる必要があります。

    転送コンテキストは、パケットの帯域外 (OOB) データに存在します。 送信元ポート、1つまたは複数の宛先ポートの配列など、パケットの転送情報が含まれています。

    転送コンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

-   拡張機能は、 [*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)を呼び出すことによって、既存のソースポートを含む OOB データを元のパケットから複製されたパケットにコピーする必要があります。 拡張機能がパケットを受信データパスに挿入することを計画している場合は、元のパケットの OOB データから宛先ポートもコピーする必要があります。

    OOB データをコピーする場合、拡張機能は次のガイドラインに従う必要があります。

    -   フィルター拡張機能で、パケットを受信データパスに挿入する予定の場合、 [*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)を呼び出して、NDIS\_スイッチ\_コピー\_NBL\_INFO\_フラグを使用して\_変換先を保持する必要があります。フラグが指定されていません。\_ これにより、元のパケットの宛先ポートが複製されたパケットにコピーされません。 フィルター拡張機能がこのパケットを受信データパスに挿入すると、基になる転送拡張機能 (ドライバースタックで有効になっている場合) または拡張可能スイッチのミニポートエッジのいずれかによって、送信先ポートがパケットに追加されます。

    -   フィルター拡張機能によって、パケットを送信データパスに挿入する予定の場合、 [*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)を呼び出して、NDIS\_スイッチ\_コピー\_NBL\_INFO\_フラグを指定し\_変換先を保持する必要があります。フラグが指定されました。\_ これにより、元のパケットの宛先ポートが複製されたパケットにコピーされます。

-   フィルター拡張機能が、送信データパスから取得されたパケットの複製または複製を行う場合は、 [*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)\_を呼び出した後で、パケットの宛先ポートを変更し\_コピー\_NBL をコピーすることができます。指定された\_送信先フラグを保持\_ための\_情報\_フラグ。 この手順の詳細については、「[パケットの拡張可能スイッチのソースポートデータを変更する](modifying-a-packet-s-extensible-switch-source-port-data.md)」を参照してください。

-   転送拡張機能が、受信データパスから取得されたパケットの複製または複製を行う場合、パケットを受信データパスに挿入する前に、そのパケットに新しい宛先ポートを追加する必要があります。 この手順の詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

-   拡張機能が[*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)を呼び出した後、パケットには元のパケットに含まれていたのと同じ発信元ポート情報が割り当てられます。

    拡張機能は[*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)を呼び出して、パケットの帯域外 (OOB) データ内の送信元ポート情報を変更できます。

    この拡張機能では、パケットが特定のポートから送信されたものとして扱われるようにすることができます。 これにより、そのポートのポリシーをパケットに適用できます。 この拡張機能は、 [*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)を呼び出してパケットの送信元ポートを変更します。

    ただし、この拡張機能では、パケットの発信元ポート識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に割り当てることが必要になる場合があります。 たとえば、外部ネットワーク上のデバイスに送信される専用の制御パケットに対して、発信元ポートの識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に設定することができます。

-   標準の NDIS データパスでは、非拡張可能スイッチ OOB データは、パケットが送信または受信のどちらとして示されているかによって異なる値を持つことがよくあります。 たとえば、 [**NDIS\_IPSEC\_オフロード\_V2\_ヘッダー\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) OOB data は、送信と受信の特定の構造を結合したものです。

    拡張可能なスイッチのデータパスでは、すべてのパケットが、送信と受信の両方として拡張機能のドライバースタックを経由して移動されます。 このため、パケットの[**NET\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造内の非拡張スイッチの OOB データは、ドライバースタックを介してフローが実行されている間、送信形式または受信形式のいずれかになります。

    この OOB データの形式は、拡張可能スイッチでパケットが到着したソース拡張可能なスイッチポートによって異なります。 ソースポートが外部ネットワークアダプターに接続されている場合、非拡張スイッチ OOB データは受信形式になります。 その他のポートの場合、この OOB データは送信形式になります。

    送信元ポートの情報は、パケットの Net\_buffer\_[**list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の OOB データ内の[ **\_詳細\_net\_buffer\_list\_INFO\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)されるように、NDIS\_スイッチに格納されます。データ. 拡張機能は、NET\_BUFFER\_LIST を使用してデータを取得し[ **\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロを使用します。

    **メモ** 拡張機能によってパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造が複製される場合、oob データを追加または変更する場合は、非拡張スイッチ oob データを考慮に入れる必要があります。 拡張機能は、 [*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)を呼び出して、送信元パケットから複製されたパケットにすべての OOB データをコピーできます。 この関数は、データがパケットにコピーされるときに、OOB の送信または受信形式を維持します。



-   拡張機能によってパケットが複製されると、複製されたパケットデータは、Hyper-v の親パーティションの親オペレーティングシステムのローカルまたは*信頼さ*れたメモリに配置されます。 このメモリには、子パーティションからアクセスすることはできません。 そのため、そのパーティションで実行されているゲストオペレーティングシステムによる同期されていない更新からは、"安全" と見なされます。

    元のパケットが複製された後、拡張機能は NDIS\_スイッチを取得する必要があります。これは、複製されたパケット内の[ **\_詳細\_net\_BUFFER\_LIST\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)を net\_を使用して転送します。 [**バッファー\_一覧\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロ。 拡張機能では、 **IsPacketDataSafe**メンバーを TRUE に設定する必要があります。 これは、すべてのパケットデータが信頼できるメモリ内にあることを指定します。

フィルターおよび転送拡張機能は、次のガイドラインに従って、複製されたパケットを受信または送信データパスに挿入する必要があります。

-   拡張機能は、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出して、複製されたパケットを受信データパスに挿入する必要があります。 拡張機能では、適切な拡張可能なスイッチフラグ設定を使用して*Sendflags*パラメーターを設定する必要があります。 これらのフラグ設定の詳細については、「 [Hyper-v 拡張可能スイッチの送信フラグと受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)」を参照してください。

    NDIS が、複製されたパケットの送信要求を完了するために拡張機能の[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出す場合、拡張機能は[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)を呼び出して、割り当てられた転送コンテキストを解放する必要があります。 この拡張機能は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を解放または再利用する前に、この操作を行う必要があります。

    **メモ** 送信データパスから取得したパケットのパケットデータまたは送信元ポートを変更する場合、拡張機能は、複製されたパケットを受信データパスに挿入する必要があります。 また、パケットの宛先ポートが保持されていない場合は、複製されたパケットを受信データパスに挿入する必要があります。



-   この拡張機能は、 [**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を呼び出して、複製されたパケットを送信データパスに挿入する必要があります。 拡張機能では、適切な拡張可能なスイッチフラグ設定を使用して*receiveflags*パラメーターを設定する必要があります。

    NDIS が拡張機能の[*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数を呼び出して、複製されたパケットの受信要求を完了する場合、拡張機能は[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)を呼び出してから、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を解放または再利用する必要があります。

    **メモ** 転送拡張機能が[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を呼び出す前に、複製されたパケットの宛先ポートを決定し、このデータをパケットの OOB データに追加する必要があります。



-   拡張機能によってパケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造が複製される場合、複製されたパケットの送信または受信要求が完了するまで、元のパケットの**net\_buffer\_list**構造の所有権を保持する必要があります。 この拡張機能では、複製されたパケットの**net\_buffer\_list**構造体の**ParentNetBufferList**メンバーを使用して、元のパケットの**net\_buffer\_list**構造にリンクする必要があります。

    **メモ** NDIS 6.30 (Windows Server 2012) では、拡張機能は**ParentNetBufferList**メンバーを使用して元のパケットにリンクできますが、これを行う必要はありません。 NDIS 6.40 (Windows Server 2012 R2) 以降では、 **ParentNetBufferList**メンバーを使用して元のパケットにリンクするために、拡張機能が必要です。

    複製されたパケットの送信または受信要求が完了すると、拡張機能は元のパケットの送信または受信要求を完了する必要があります。

    **メモ** 拡張機能によってパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造が複製されている場合、複製された後に元のパケットの送信または受信要求を完了することができます。

-   拡張機能がパケットを複製する場合は、元のパケットが複製されるとすぐに、送信または受信の要求を完了できます。

転送またはフィルター拡張によって送信データパス内のパケットが取得される場合、その拡張機能によってパケットデータが変更されたり、ソースポートが変更されたりした場合、このデータパスには複製されたバージョンのパケットを挿入できません。 ただし、拡張機能はこれらのパケットを受信データパスに挿入できます。 これにより、拡張可能なスイッチのデータパスを介してパケットを適切に転送およびフィルター処理できます。

**メモ** フィルター拡張機能は、パケットの宛先ポートが保持されていない場合にのみ、複製されたパケットを受信データパスに挿入できます。

たとえば、複数の宛先ポートを持つパケットが拡張スイッチの送信データパスで取得されたとします。 データのカプセル化など、1つの宛先ポートで特別な処理が必要な場合、転送またはフィルター拡張機能は次の手順に従ってこれを処理します。

1.  特別な処理を必要とするポートへのパケット配信を除外します。 この拡張機能では、宛先ポートの[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体の**IsExcluded**メンバーを1の値に設定することによってこれを行います。 この手順の詳細については、「[拡張可能スイッチの接続先ポートへのパケット配信の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)」を参照してください。

2.  元のパケットを複製し、パケットデータに対して必要な処理を実行します。

    **メモ** フィルター拡張機能では、複製されたパケットの宛先ポートを追加しないでください。 このデータは、拡張可能なスイッチの転送拡張機能またはミニポートエッジによって後で追加されます。

3.  [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出して、送信データパスの元のパケットを転送します。

4.  [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出して、複製されたパケットを受信データパスに挿入します。

拡張可能なスイッチの受信と送信のデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

**メモ** キャプチャ拡張機能はパケットトラフィックを複製できません。 ただし、パケットトラフィックが発生する可能性があります。 詳細については、「[発信元パケットトラフィック](originating-packet-traffic.md)」を参照してください。











