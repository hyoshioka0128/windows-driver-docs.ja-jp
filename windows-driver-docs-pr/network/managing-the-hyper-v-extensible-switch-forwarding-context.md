---
title: Hyper-V 拡張可能スイッチ転送コンテキストの管理
description: Hyper-V 拡張可能スイッチ転送コンテキストの管理
ms.assetid: 63FBEBFA-BD57-4350-89C3-9F0FAAA18973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8731474d11f5d40b98e1f1136466a6bf82e16f8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369186"
---
# <a name="managing-the-hyper-v-extensible-switch-forwarding-context"></a>Hyper-V 拡張可能スイッチ転送コンテキストの管理


**注**このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。



[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造に、HYPER-V 拡張可能スイッチのデータ パスを通過する各パケットには、アウト オブ バンド (OOB) データが含まれています。 このデータは、パケットが発信された場所、およびパケット配信のための 1 つまたは複数の宛先ポートからの発信元ポートを指定します。 この OOB データと呼ばれる、*転送コンテキスト拡張可能スイッチ*します。

**注**拡張可能スイッチ転送コンテキストが異なる、 [ **NET\_バッファー\_一覧\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造体。 これにより、拡張機能転送コンテキストの影響を与えずに、独自のコンテキストの構造を割り当てることができます。

拡張可能スイッチ転送コンテキストに割り当てられ、次の方法で解放。

-   ネットワーク アダプターから、パケットの拡張可能スイッチが到着すると、拡張可能スイッチのインターフェイスが転送コンテキストを割り当て、パケットに関連付けます[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

    インターフェイスがパケットの転送コンテキストを解放するパケットは、その宛先ポートに配信は、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

-   呼び出す前に、転送コンテキストを割り当てる必要があります、新規または複製されたパケットは、拡張可能スイッチの拡張機能は、拡張可能スイッチのデータ パスに挿入する場合、 [ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)します。

    拡張機能の割り当て後に、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造新しいまたは複製されたパケットの場合は、呼び出す必要があります、 [ *AllocateNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数にパケットを転送コンテキストを割り当てられません。 拡張機能を呼び出す必要があります、要求の送信パケットが完了したら、 [ *FreeNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)解放または再利用する前に、 **NET\_バッファー\_一覧**構造体。

    **注**、拡張機能を呼び出すと[ *AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)、パケットの発信元ポートに設定されている**NDIS\_スイッチ\_既定\_ポート\_ID**します。 これは、パケットが、拡張可能スイッチ ポートに到着するのではなく、拡張機能から発信されたことを指定します。 特定の条件下で、拡張機能が、パケットの発信元ポートを変更するとする可能性があります。 詳細については、次を参照してください。[パケットの拡張可能スイッチ ソース ポート データを変更する](modifying-a-packet-s-extensible-switch-source-port-data.md)します。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの送信と受信操作](hyper-v-extensible-switch-send-and-receive-operations.md)します。

すべての拡張可能スイッチ拡張機能は、次の拡張可能スイッチ パケットの転送のコンテキスト内でデータにアクセスするハンドラー関数を呼び出すことができます。

<a href="" id="allocatenetbufferlistforwardingcontext"></a>[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)  
拡張可能スイッチ転送コンテキストを割り当て、準備、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)送信用の構造または拡張可能スイッチ内の操作を受信します。

<a href="" id="copynetbufferlistinfo"></a>[*CopyNetBufferListInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_copy_net_buffer_list_info)  
コピー ソース パケットの転送コンテキスト[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)対象パケットの構造体**NET\_バッファー\_リスト**構造体。 このデータには、拡張可能スイッチ ソース ポートおよびネットワーク アダプターの情報が含まれます。 対象の拡張可能スイッチのポート情報は、移行先のパケットにもコピーできます。

<a href="" id="freenetbufferlistforwardingcontext"></a>[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)  
拡張可能スイッチ転送コンテキストでリソースを解放する[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 このデータは、送信に使用されたまたは HYPER-V 拡張可能スイッチでの操作を受信し、呼び出すことによって割り当てられていた、 [ *AllocateNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数。

<a href="" id="getnetbufferlistdestinations"></a>[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)  
パケットが転送コンテキストから宛先ポートを返します[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造体。

転送拡張機能は、パケットが、NVGRE パケットでない限り、パケットの宛先ポートを追加する責任を負います。 (詳細については、次を参照してください[ハイブリッド転送](hybrid-forwarding.md)。)。拡張機能は、次の拡張可能スイッチを追加または変換先ポート、パケットの転送のコンテキスト内での更新のハンドラー関数を呼び出します。

<a href="" id="addnetbufferlistdestination"></a>[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)  
コンテキストの領域で指定されているパケットを転送する拡張可能スイッチに 1 つの宛先を追加、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造体。

**注**この呼び出しを転送する、変更をコミットするコンテキストの領域。 この場合、転送拡張機能を呼び出す必要はありません[ *UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)します。

<a href="" id="grownetbufferlistdestinations"></a>[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)  
転送先のポート配列のサイズを大きくのパケットのコンテキスト領域[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)構造体。

<a href="" id="updatenetbufferlistdestinations"></a>[*UpdateNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)  
拡張機能は、パケットの 1 つまたは複数の拡張可能スイッチ宛先ポートに加えられた変更をコミットします。 この関数は更新のパケットが転送コンテキスト[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)これらの変更を含む構造体。

**注**宛先ポートが削除された機能とのみにすることはできません転送拡張機能が転送コンテキストに宛先ポートの変更をコミットした後、 **IsExcluded**の宛先ポートのメンバー [**NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造を変更することができます。 詳細については、次を参照してください。[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)します。

## <a name="related-topics"></a>関連トピック


[HYPER-V 拡張可能スイッチのコンテキストの転送](hyper-v-extensible-switch-forwarding-context.md)

[HYPER-V 拡張可能スイッチのコンテキストのデータ型の転送](hyper-v-extensible-switch-forwarding-context-data-types.md)










