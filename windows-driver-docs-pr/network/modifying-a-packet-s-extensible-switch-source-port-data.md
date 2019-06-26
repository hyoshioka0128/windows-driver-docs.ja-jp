---
title: パケットの拡張可能スイッチの発信元ポート データの変更
description: パケットの拡張可能スイッチの発信元ポート データの変更
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1539fab658bc32976b02b68448a983b12623424
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372593"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポート データの変更


HYPER-V 拡張可能スイッチの発信元ポートが指定された、 **SourcePortId**内のメンバー、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体。 この構造体の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

拡張可能スイッチ拡張機能は、パケットの送信元ポートの識別子を変更するための次のガイドラインに従う必要があります。

-   拡張可能スイッチ拡張機能を呼び出す必要があります[ *SetNetBufferListSource* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)パケットの発信元ポートを変更します。 拡張機能が直接変更する必要があります、 **SourcePortId**のメンバー、 [ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体。

-   呼び出す必要がありますが、拡張機能を作成または、パケットを複製する場合、 [ *AllocateNetBufferListForwardingContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数の呼び出し後[ **NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlist). この関数は、OOB データ パケットの情報を転送するために使用されるコンテキスト スイッチの拡張可能な領域を割り当てます。

    拡張機能を呼び出すと[ *AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)、 **SourcePortId**に設定されているメンバー **NDIS\_スイッチ\_既定の\_ポート\_ID**します。 これは、パケットが、拡張可能スイッチ ポートに到着するのではなく、拡張機能から発信されたことを指定します。

    パケットの発信元ポートと**NDIS\_切り替える\_既定\_ポート\_ID**は拡張可能スイッチ拡張機能のデータ パス特権によって扱われ、信頼されています。 このようなトラフィックは、その他の発信元ポートからのパケットに適用されるポリシーに従う必要はありません。 たとえば、パケットの送信元ポート識別子を**NDIS\_切り替える\_既定\_ポート\_ID**基になるで適用される拡張可能スイッチの組み込みポリシーをバイパス拡張可能スイッチのミニポート エッジです。 これらのポリシーは、アクセス制御リスト (Acl) とサービスの品質 (QoS)。

    発信元ポートを使用すると、拡張機能には、トラフィックのパケットが発信、 **NDIS\_スイッチ\_既定\_ポート\_ID**注意して慎重にします。 ほとんどの場合、拡張機能は拡張可能スイッチのアクティブなポートに送信元ポートの識別子を変更する必要があります。 これにより、パケットに適用するには、そのポートのポリシーができます。

    ただし、場合があります、拡張機能が、発信元ポートを使用して、 **NDIS\_スイッチ\_既定\_ポート\_ID**パケットの発生元します。 たとえば、拡張機能を使用する、物理または仮想ネットワーク上の宛先に送信する必要のあるコントロールのパケットの発生元**NDIS\_スイッチ\_既定\_ポート\_ID**ソース ポートの識別子。 こうこと、パケットはいないフィルター処理され、拡張可能スイッチ ドライバー スタック内の基になる拡張機能によって拒否されます。

 

 





