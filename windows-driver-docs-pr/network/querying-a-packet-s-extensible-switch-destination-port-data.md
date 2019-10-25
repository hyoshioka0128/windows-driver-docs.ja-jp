---
title: パケットの拡張可能スイッチの宛先ポート データのクエリ
description: パケットの拡張可能スイッチの宛先ポート データのクエリ
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dd5ed6fc79176bc7568dd65c37ab991320608d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844886"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>パケットの拡張可能スイッチの宛先ポート データのクエリ


各 Hyper-v 拡張可能スイッチの宛先ポートは、ndis\_スイッチによって指定されます。 Ndis\_スイッチ内の[ **\_port\_destination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)要素によって\_[**転送先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造に転送されます. この配列は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の帯域外 (OOB) 転送コンテキストに含まれています。 このコンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

拡張可能なスイッチ拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)関数を呼び出して、パケットの NET 内の[ **\_宛先\_配列構造を転送\_、NDIS\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)へのポインターを取得し[ **\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体。 個々の[**ndis\_スイッチ\_ポート\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)この構造内の宛先要素には、 [**ndis\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)を使用してアクセスできます\_\_配列\_インデックスマクロ.

パフォーマンスを向上させるために、転送拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)の代わりに[*GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数を呼び出して、 [**NDIS\_\_\_スイッチへのポインターを取得します。変換先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 この拡張機能は、パケットの OOB データに追加の配列要素が必要であると判断した場合に、これを行います。 詳細については、「[拡張可能スイッチの宛先ポートデータをパケットに追加](adding-extensible-switch-destination-port-data-to-a-packet.md)する」を参照してください。

**注**  拡張可能スイッチの送信データパスから取得したパケットにのみ、宛先ポート情報が含まれます。 詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 

 





