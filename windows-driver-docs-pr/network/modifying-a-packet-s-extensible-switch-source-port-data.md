---
title: パケットの拡張可能スイッチの発信元ポート データの変更
description: パケットの拡張可能スイッチの発信元ポート データの変更
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8296ae6c43256124504d2e4762ca6c6917c1825f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844226"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポート データの変更


Hyper-v 拡張可能スイッチのソースポートは、NDIS\_スイッチの**SourcePortId**メンバーによって指定されます。 [ **\_転送\_詳細\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体です。 この構造体は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の帯域外 (OOB) 転送コンテキストに含まれています。 このコンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

拡張可能なスイッチ拡張機能は、次のガイドラインに従ってパケットの発信元ポート識別子を変更する必要があります。

-   拡張可能なスイッチ拡張機能は、パケットの送信元ポートを変更するために[*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)を呼び出す必要があります。 拡張機能では、NDIS\_スイッチの**SourcePortId**メンバーを直接変更しないでください。 [ **\_詳細\_NET\_BUFFER\_LIST\_INFO 構造\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)します。

-   拡張機能がパケットを作成または複製する場合は、 [**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)を呼び出した後に[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)関数を呼び出す必要があります。 この関数は、パケットの転送情報に使用される OOB データの拡張可能なスイッチコンテキスト領域を割り当てます。

    拡張機能が[*AllocateNetBufferListForwardingContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context)を呼び出すと、 **SourcePortId**メンバーは、**既定\_ポート\_ID**に設定され\_、NDIS\_スイッチに設定されます。 これは、拡張可能なスイッチポートではなく、拡張機能からパケットが送信されたことを示します。

    NDIS\_スイッチの発信元ポートを持つパケット **\_既定の\_ポート\_ID**は、拡張可能スイッチ拡張機能のデータパスで privileged および trusted として扱われます。 このようなトラフィックは、他の送信元ポートからのパケットに適用されるポリシーには適用されません。 たとえば、NDIS\_の発信元ポート id を持つパケットは、**既定の\_ポート\_ID\_** 、拡張可能スイッチの基になるミニポートエッジによって適用される組み込みの拡張可能スイッチポリシーをバイパスします。 これらのポリシーには、アクセス制御リスト (Acl) やサービスの品質 (QoS) などがあります。

    拡張機能がパケットトラフィックの発信元である場合は、NDIS の発信元ポートを使用する必要があります。これは、**既定\_ポート\_ID を注意深く\_\_スイッチ**を慎重に行う必要があります。 ほとんどの場合、拡張機能は、ソースポート識別子を拡張可能スイッチのアクティブポートに変更する必要があります。 これにより、そのポートのポリシーをパケットに適用できます。

    ただし、拡張機能が NDIS\_の発信元ポートを使用する必要がある場合もあります。これは、発信元のパケットに対して、**既定\_ポート\_ID を\_** ます。 たとえば、物理ネットワークまたは仮想ネットワーク上の宛先に送信する必要がある制御パケットが拡張機能によって生成される場合、NDIS\_スイッチを使用する必要があります。これは、発信元ポート識別子に対して、**既定の\_ポート\_ID**を使用する場合\_です。 これにより、拡張可能なスイッチドライバースタックの基になる拡張機能によって、パケットがフィルター処理および拒否されることがなくなります。

 

 





