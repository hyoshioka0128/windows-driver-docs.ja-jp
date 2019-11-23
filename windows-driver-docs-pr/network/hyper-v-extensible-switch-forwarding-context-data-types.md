---
title: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
description: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
ms.assetid: B5377411-C6F0-47BE-BD45-534AC784ED76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 374b18d95f001592b01b9a74f98aa686334a98bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823911"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 拡張可能スイッチ転送コンテキスト データの種類


Hyper-v 拡張可能スイッチのデータパスを通過する各パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、帯域外 (OOB) データが含まれています。 このデータは、パケットの発信元ポート、およびパケット配信用の1つ以上の宛先ポートを指定します。 この OOB データは、*拡張可能なスイッチ転送コンテキスト*と呼ばれます。

パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造内の拡張可能なスイッチ転送コンテキストにアクセスするために、次のデータ型が宣言されています。

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS\_スイッチ\_転送\_詳細\_NET\_BUFFER\_LIST\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
これは、パケットの転送特性を含む64ビットの共用体です。 このデータには、パケットの発信元ポートとネットワークアダプター接続の識別子が含まれます。 このデータには、宛先ポート配列で使用可能な未使用の要素の数も含まれます。

拡張可能なスイッチ拡張機能では、NET\_BUFFER\_LIST を使用してこのデータにアクセスできます。 [ **\_転送\_詳細マクロ\_切り替える**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)ことができます。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS\_スイッチ\_転送先\_配列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
この構造体は、パケットの宛先ポート配列を定義します。 この配列の各要素は、 [**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)構造体として書式設定されます。

[**NDIS\_スイッチ\_転送\_宛先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造には、要素の合計数と配列内の使用されている要素の数を指定するメンバーが含まれます。

拡張可能なスイッチ拡張機能は、 [*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)関数を呼び出すことによって、この配列を取得できます。 ドライバーが複数の宛先ポートを持つパケットの配列の要素を追加または変更する場合は、 [*Updatenetbufferlistdestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)関数を呼び出す必要があります。 この関数は、パケットの転送コンテキスト内の宛先ポート配列にこれらの変更をコミットします。

宛先ポートが1つのみのパケットに変更をコミット**する  、** ドライバーが[*AddNetBufferListDestination*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)関数を呼び出す方が効率的です。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS\_スイッチ\_ポート\_宛先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)  
この構造体は、パケットの宛先ポートを定義します。 1つの宛先ポートを持つパケットの場合、宛先ポートアレイには、 [**NDIS\_スイッチ\_port\_destination**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_port_destination)要素が1つだけあります。 複数の宛先ポートを持つパケットの場合、配列にはこれらの要素が1つ以上含まれています。

拡張可能なスイッチ拡張機能が[*GetNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)を呼び出してパケットの宛先ポート配列を取得した後は、 [ **\_array\_INDEX マクロで、NDIS\_スイッチ\_port\_destination\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)を使用して、配列内の個々の要素にアクセスできます。

 

 





