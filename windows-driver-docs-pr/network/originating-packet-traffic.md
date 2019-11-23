---
title: パケット トラフィックの生成
description: パケット トラフィックの生成
ms.assetid: 613C7E82-387D-47AE-A699-A799087D3C1D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50081c0012b757f426b66c5e600910df1b7897c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843757"
---
# <a name="originating-packet-traffic"></a>パケット トラフィックの生成


このトピックでは、Hyper-v 拡張機能によって新しいパケットが生成され、拡張可能なスイッチのデータパスに挿入されるしくみについて説明します。

**注**  このページでは、 [Hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。

 

**注**  拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは拡張*可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。 拡張機能の詳細については、「 [Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)」を参照してください。

 

拡張可能なスイッチ拡張機能では、拡張可能なスイッチの受信データパスに新しいパケットのみを挿入できます。 これにより、拡張可能なスイッチインターフェイスは、これらのパケットをフィルター処理し、適切に転送できます。 拡張機能は、次のガイドラインに従って、新しいパケットを受信データパスに挿入する必要があります。

-   拡張機能では、最初に新しいパケットに対して[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を割り当てる必要があります。

-   拡張機能によって、新しいパケットに対して[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体が割り当てられた後、 [*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) handler 関数を呼び出して、パケットの拡張可能なスイッチ転送コンテキストを割り当てる必要があります。

    転送コンテキストは、パケットの帯域外 (OOB) データに存在します。 送信元ポート、1つまたは複数の宛先ポートの配列など、パケットの転送情報が含まれています。

    転送コンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

-   拡張機能が[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)を呼び出した後、パケットの送信元ポートは**NDIS\_スイッチ\_既定\_ポート\_ID**に設定されます。 NDIS\_スイッチの発信元ポート識別子を持つパケット **\_既定の\_ポート\_ID**は信頼されており、アクセス制御リスト (acl) やサービスの品質 (QoS) などの拡張可能なスイッチポートポリシーをバイパスします。

    この拡張機能では、パケットが特定のポートから送信されたものとして扱われるようにすることができます。 これにより、そのポートのポリシーをパケットに適用できます。 この拡張機能は、 [*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)を呼び出してパケットの送信元ポートを変更します。

    ただし、この拡張機能では、パケットの発信元ポート識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に割り当てることが必要になる場合があります。 たとえば、外部ネットワーク上のデバイスに送信される専用の制御パケットに対して、発信元ポートの識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に設定することができます。

-   転送拡張機能が受信データパスに新しいパケットを送信する場合は、パケットの宛先ポートを決定する必要があります。 この手順の詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

    キャプチャまたはフィルター拡張機能が新しいパケットに新しい宛先ポートを追加できない  に**注意**してください。

     

-   拡張機能によって新しいパケットが作成されると、パケットデータは、Hyper-v の親パーティションの親オペレーティングシステムのローカルまたは*信頼さ*れたメモリに配置されます。 このメモリには、子パーティションからアクセスできません。 そのため、そのパーティションで実行されているゲストオペレーティングシステムによる同期されていない更新からは、"安全" と見なされます。

    拡張機能は、 [**net\_buffer\_list**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)\_\_\_\_detail マクロを使用して、新しいパケットの\_[ **\_詳細\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)するために、NDIS\_スイッチを取得する必要があります。\_\_ 拡張機能では、 **IsPacketDataSafe**メンバーを TRUE に設定する必要があります。 これは、すべてのパケットデータが信頼できるメモリ内にあることを指定します。

-   拡張機能が[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出してパケットを受信データパスに挿入するときは、 *Flags*パラメーターに適切な拡張可能なスイッチフラグ設定を設定する必要があります。 これらのフラグ設定の詳細については、「 [Hyper-v 拡張可能スイッチの送信フラグと受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)」を参照してください。

-   NDIS が拡張機能の[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)関数を呼び出して新しいパケットの送信要求を完了する場合、拡張機能は[*FreeNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_free_net_buffer_list_forwarding_context)を呼び出して、割り当てられた転送コンテキストを解放する必要があります。 この拡張機能は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)構造体を解放または再利用する前に、この操作を行う必要があります。

拡張可能なスイッチの受信と送信のデータパスの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 





