---
title: Hyper-V 拡張可能スイッチ転送コンテキストの管理
description: Hyper-V 拡張可能スイッチ転送コンテキストの管理
ms.assetid: 63FBEBFA-BD57-4350-89C3-9F0FAAA18973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6585863b7de553d8df2e4cb866f27668eebf42ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844109"
---
# <a name="managing-the-hyper-v-extensible-switch-forwarding-context"></a>Hyper-V 拡張可能スイッチ転送コンテキストの管理


**メモ** このページでは、 [hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。



Hyper-v 拡張可能スイッチのデータパスを通過する各パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、帯域外 (OOB) データが含まれています。 このデータは、パケットの発信元ポート、およびパケット配信用の1つ以上の宛先ポートを指定します。 この OOB データは、*拡張可能なスイッチ転送コンテキスト*と呼ばれます。

**メモ** 拡張可能なスイッチ転送コンテキストは、 [**NET\_BUFFER\_LIST\_context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体とは異なります。 これにより、拡張機能では、転送コンテキストに影響を与えずに独自のコンテキスト構造を割り当てることができます。

拡張可能なスイッチ転送コンテキストは、次の方法で割り当てられ、解放されます。

-   ネットワークアダプターから拡張可能スイッチにパケットが到着すると、拡張可能なスイッチインターフェイスによって転送コンテキストが割り当てられ、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられます。

    パケットが宛先ポートに配信されると、インターフェイスはパケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造から転送コンテキストを解放します。

-   拡張可能なスイッチ拡張機能によって、拡張可能なスイッチのデータパスに新しいパケットまたは複製されたパケットが挿入された場合、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出す前に、転送コンテキストを割り当てる必要があります。

    拡張機能によって、新しいパケットまたは複製されたパケットに対して[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体が割り当てられた後、 [*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数を呼び出してパケットの転送コンテキストを割り当てる必要があります。 パケット送信要求が完了したら、拡張機能は[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)を呼び出してから、 **NET\_BUFFER\_LIST**構造体を解放するか再利用する必要があります。

    **メモ** 拡張機能が[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)を呼び出すと、パケットの送信元ポートが**NDIS\_スイッチ\_既定の\_ポート\_ID**に設定されます。 これは、拡張可能なスイッチポートではなく、拡張機能からパケットが送信されたことを示します。 特定の条件下では、拡張機能によってパケットの送信元ポートを変更することが必要になる場合があります。 詳細については、「[パケットの拡張可能スイッチのソースポートデータを変更する](modifying-a-packet-s-extensible-switch-source-port-data.md)」を参照してください。

    詳細については、「 [Hyper-v 拡張可能スイッチの送信と受信の操作](hyper-v-extensible-switch-send-and-receive-operations.md)」を参照してください。

拡張可能なすべてのスイッチ拡張機能は、パケットの転送コンテキスト内のデータにアクセスするために、次の拡張可能なスイッチハンドラー関数を呼び出すことができます。

<a href="" id="allocatenetbufferlistforwardingcontext"></a>[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)  
拡張可能スイッチの転送コンテキストを割り当て、拡張可能なスイッチ内の送信操作または受信操作に対して、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を準備します。

<a href="" id="copynetbufferlistinfo"></a>[*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)  
送信元パケットの[**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体から送信先パケットの**net\_buffer\_list**構造体に転送コンテキストをコピーします。 このデータには、拡張可能なスイッチソースポートとネットワークアダプターの情報が含まれます。 拡張可能スイッチの接続先ポート情報を宛先パケットにコピーすることもできます。

<a href="" id="freenetbufferlistforwardingcontext"></a>[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)  
[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の拡張可能スイッチの転送コンテキストで、リソースを解放します。 このデータは、Hyper-v 拡張可能スイッチでの送信操作または受信操作に使用され、以前は[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数を呼び出して割り当てられていました。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体の転送コンテキストから宛先ポートを返します。

パケットが NVGRE パケットでない限り、転送拡張機能はパケットの宛先ポートを追加する必要があります。 (詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください)。拡張機能は、次の拡張可能なスイッチハンドラー関数を呼び出して、パケットの転送コンテキスト内の宛先ポートを追加または更新します。

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体によって指定されたパケットの拡張可能スイッチ転送コンテキスト領域に1つの変換先を追加します。

**メモ** この呼び出しは、転送コンテキスト領域に変更をコミットします。 この場合、転送拡張機能は[*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)を呼び出す必要はありません。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体の転送コンテキスト領域内の宛先ポート配列のサイズを大きくします。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
拡張機能によって、1つまたは複数の拡張可能スイッチが、パケットの宛先ポートに対して行われた変更をコミットします。 この関数は、これらの変更を使用して、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造の転送コンテキストを更新します。

**メモ** 転送拡張機能によって宛先ポートの変更が転送コンテキストにコミットされた後、宛先ポートを削除することはできず、宛先ポートの NDIS\_の**IsExcluded**メンバのみが\_ポートを切り替えることができ[ **\_ターゲット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造は変更できます。 詳細については、「[拡張可能スイッチの接続先ポートへのパケット配信の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)」を参照してください。

## <a name="related-topics"></a>関連トピック


[Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)

[Hyper-v 拡張可能スイッチ転送コンテキストデータ型](hyper-v-extensible-switch-forwarding-context-data-types.md)










