---
title: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
description: Hyper-V 拡張可能スイッチ転送コンテキスト データの種類
ms.assetid: B5377411-C6F0-47BE-BD45-534AC784ED76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fda88cb4e96296bb1105dcea0e450ea41e3c320b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383697"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 拡張可能スイッチ転送コンテキスト データの種類


[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造に、HYPER-V 拡張可能スイッチのデータ パスを通過する各パケットには、アウト オブ バンド (OOB) データが含まれています。 このデータは、パケットが発信された場所、およびパケット配信のための 1 つまたは複数の宛先ポートからの発信元ポートを指定します。 この OOB データと呼ばれる、*転送コンテキスト拡張可能スイッチ*します。

パケットの内で拡張可能スイッチ転送コンテキストにアクセスする次のデータ型が宣言されている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS\_SWITCH\_FORWARDING\_DETAIL\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
これは、パケットの転送の特性を含む 64 ビットの和集合です。 このデータには、パケットが元のソース ポートおよびネットワーク アダプター接続の識別子が含まれています。 このデータには、コピー先のポートの配列で利用できる未使用の要素の数も含まれています。

拡張可能スイッチ拡張機能を使用してこのデータにアクセスできる、 [ **NET\_バッファー\_一覧\_切り替える\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロ。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
この構造体は、パケットの宛先ポート配列を定義します。 この配列内の各要素として書式設定、 [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体。

[ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体には、現在の合計数を指定するメンバーが含まれています。配列で使用される要素の数と要素の数。

拡張可能スイッチ拡張機能は呼び出すことでこの配列を取得することができます、 [ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)関数。 場合は、ドライバーを追加または変更には、複数の宛先ポートでのパケットの配列内の要素、呼び出す必要があります、 [ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)関数。 この関数は、パケットの転送のコンテキストでのコピー先ポートの配列にそれらの変更をコミットします。

**注**  を 1 つだけの宛先ポートでのパケットに変更をコミットするには、ドライバーを呼び出す方が効率的、 [ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)関数。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS\_スイッチ\_ポート\_変換先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)  
この構造体は、パケットの宛先ポートを定義します。 1 つの宛先ポート、パケットの 1 つしかない[ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)先ポートの配列内の要素。 複数の宛先ポートとパケットの場合は、配列内のこれらの要素の 1 つ以上です。

拡張機能が呼び出された後、拡張可能スイッチに[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)にパケットの宛先ポートの配列を取得するには、を使用して、配列内の個々の要素をアクセス[ **NDIS\_スイッチ\_ポート\_先\_で\_配列\_インデックス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)マクロ。

 

 





