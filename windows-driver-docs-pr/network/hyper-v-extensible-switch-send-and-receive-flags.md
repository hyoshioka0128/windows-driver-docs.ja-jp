---
title: Hyper-V 拡張可能スイッチ送信および受信フラグ
description: Hyper-V 拡張可能スイッチ送信および受信フラグ
ms.assetid: FBA506EC-4E9F-4964-9C9C-FF4910DDA908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23216bd95306e31cbe14d03e8217d82346cf52ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386537"
---
# <a name="hyper-v-extensible-switch-send-and-receive-flags"></a>Hyper-V 拡張可能スイッチ送信および受信フラグ


**注**  このページは、情報とでのダイアグラムに精通していることを前提としています。 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)します。

 

HYPER-V 拡張可能スイッチのデータ パスの上に移動するパケット トラフィックが、次のように拡張機能によって得られます。

-   イングレス データのパスからパケットを取得する拡張機能とその[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)関数が呼び出されます。 拡張機能は、呼び出すことによって拡張機能を基になる、イングレス データ パスにパケットを転送[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)します。 フィルター処理および転送拡張機能も削除できますパケット イングレス データのパスから呼び出すことによって[ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)します。

-   出口データ パスからパケットを取得する拡張機能とその[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)関数が呼び出されます。 拡張機能が出口のデータ パスでの拡張機能を呼び出すことによって関連するパケットを転送[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)します。 フィルター処理および転送拡張機能も削除できますパケット エグレス データのパスから呼び出すことによって[ **NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)します。

次のフラグを設定することがあります、 *SendFlags*パラメーターの[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)または[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists):

<a href="" id="ndis-send-flags-switch-single-source"></a>**NDIS\_送信\_フラグ\_スイッチ\_単一\_ソース**  
このフラグが設定のリンク リストにすべてのパケット場合[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体が同じ HYPER-V 拡張可能スイッチの発信元ポートから発生しました。

NDIS を呼び出すと[ *FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)、拡張可能スイッチの拡張可能なインターフェイスが同じ発信元ポートから複数のパケットをグループ化する場合にこのフラグが設定されます。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)します。 発生元またはリンクの一覧にパケットを複製、拡張機能を追加することも[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の場合は、拡張機能を使用して、同じソースとして、その他のポートリスト内のパケットです。

**注**  場合のリンク リストには、各パケット[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体が同じソース ポートを使用して、拡張機能を設定する必要があります、**NDIS\_送信\_完了\_フラグ\_スイッチ\_単一\_ソース**フラグ、 *SendCompleteFlags*パラメーターの[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)送信要求の完了時にします。

 

<a href="" id="ndis-send-flags-switch-destination-group"></a>**NDIS\_送信\_フラグ\_スイッチ\_先\_グループ**  
このフラグが設定のリンク リストにすべてのパケットの場合[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造は、同じ拡張可能スイッチの宛先ポートに転送します。

転送拡張機能は、このフラグを使用して、リンクの一覧については[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)各パケットの判別した後、イングレス データ パスに転送する構造体宛先ポートです。 このフラグは消費し、エグレス データのパスをパケットを転送する前に、拡張可能スイッチの基になるミニポート端で削除します。

キャプチャおよび拡張機能をフィルター処理は、このフラグを使用できません。

**注**  転送拡張機能では、非 NVGRE パケットのパケットの宛先ポートのみを決定します。 パケットが、NVGRE パケットの場合は、HYPER-V ネットワーク仮想化 (HNV) のコンポーネントは、パケットの宛先ポートを決定し、パケットを転送します。 詳細については、次を参照してください。[ハイブリッド転送](hybrid-forwarding.md)します。

 

最適なパフォーマンスを転送拡張機能はこのフラグを設定を同じ宛先ポートに転送する場合は、リンク リストのすべてのパケット。 このフラグを設定して、コンテキストを転送する拡張可能スイッチに、宛先ポートと同じ要素をリンク リスト内のすべてのパケットがあること、拡張機能が受信します。

**注**  転送拡張機能は、複数のターゲットを持つパケットのリンクの一覧については、このフラグのポートを設定しない必要があります。

 

次のフラグを設定することがあります、 *ReceiveFlags*パラメーターの[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)または[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists):

<a href="" id="ndis-receive-flags-switch-single-source"></a>**NDIS\_受信\_フラグ\_スイッチ\_単一\_ソース**  
このフラグが設定のリンク リストにすべてのパケット場合[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体が同じ HYPER-V 拡張可能スイッチの発信元ポートから発生しました。

NDIS を呼び出すと[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)、拡張可能スイッチが、同じソース ポートから複数のパケットをグループ化する場合にこのフラグが設定されます。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。 発生元またはリンクの一覧にパケットを複製、拡張機能の追加もする必要があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットがある同じ場合、構造体のソースとして、他のポートリスト内のパケットです。

**注**  場合のリンク リストには、各パケット[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体を使用して、同じ発信元ポート、拡張機能を設定する必要があります、**NDIS\_返す\_フラグ\_スイッチ\_単一\_ソース**フラグ、 *ReturnFlags* のパラメーター[*FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)受信要求が完了したとき。 拡張機能このフラグを設定する必要があります、 *ReturnFlags*を呼び出す場合は、パラメーター [ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)取得されなかった戻りのパケットを複製します。

 

<a href="" id="ndis-receive-flags-switch-destination-group"></a>**NDIS\_受信\_フラグ\_スイッチ\_先\_グループ**  
このフラグが設定のリンク リストにすべてのパケットの場合[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造は、同じ拡張可能スイッチの宛先ポートに転送します。

NDIS を呼び出すと[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)にはこのフラグを設定、拡張可能スイッチが 1 つの宛先を持つ複数のパケットをグループ化する場合のポート。 最高のパフォーマンスを拡張機能にこのグループ化を維持し、を呼び出すときに、このフラグを設定[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。 発生元またはリンクの一覧にパケットを複製、拡張機能の追加もする必要があります[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体の場合は、パケットがある同じ送信先ポートとして、一覧で他のパケットをします。

**注**  拡張機能を呼び出すと[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)、これを設定する必要がありますしない、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーター。 拡張可能スイッチのインターフェイスはこのフラグを無視し、呼び出すことによって、受信を示す値を完了[ *FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)します。

 

 

 





