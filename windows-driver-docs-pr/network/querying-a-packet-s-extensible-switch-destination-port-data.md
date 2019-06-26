---
title: パケットの拡張可能スイッチの宛先ポート データのクエリ
description: パケットの拡張可能スイッチの宛先ポート データのクエリ
ms.assetid: 57D82C5E-3758-492C-A1DA-B7BC3DBE2E7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fea316b83e7afb98a77983a91edf4d1d15d0a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385439"
---
# <a name="querying-a-packets-extensible-switch-destination-port-data"></a>パケットの拡張可能スイッチの宛先ポート データのクエリ


各 HYPER-V 拡張可能スイッチの宛先ポートがで指定された、 [ **NDIS\_切り替える\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)内の要素、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 この配列は、の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

拡張可能スイッチ拡張機能の呼び出し、 [ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)へのポインターを取得する関数、 [ **NDIS\_切り替える\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)でパケットの構造体[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 個別[ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)この構造内の要素を使用してアクセスできる、 [ **NDIS\_スイッチ\_ポート\_先\_で\_配列\_インデックス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)マクロ。

パフォーマンスを向上させるには、転送拡張機能を呼び出すことができます、 [ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数の代わりに[ *GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)へのポインターを取得する、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体. 拡張機能は宛先ポートのパケットの OOB データに追加の配列の要素が必要であると判断した場合、します。 詳細については、次を参照してください。[を追加する拡張可能なスイッチ宛先ポート データ パケットに](adding-extensible-switch-destination-port-data-to-a-packet.md)します。

**注**  だけで、拡張可能スイッチのエグレス データのパスから取得したパケットには宛先ポートの情報にが含まれます。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)します。

 

 

 





