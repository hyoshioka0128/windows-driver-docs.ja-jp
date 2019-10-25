---
title: Hyper-V 拡張可能スイッチ送信および受信フラグ
description: Hyper-V 拡張可能スイッチ送信および受信フラグ
ms.assetid: FBA506EC-4E9F-4964-9C9C-FF4910DDA908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3dd16d47af8e8a2ae83c1408df9b780a9c3a0bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823828"
---
# <a name="hyper-v-extensible-switch-send-and-receive-flags"></a>Hyper-V 拡張可能スイッチ送信および受信フラグ


**注**  このページでは、 [Hyper-v の拡張可能スイッチ](overview-of-the-hyper-v-extensible-switch.md)と[ハイブリッド転送](hybrid-forwarding.md)の概要に関する情報と図について理解していることを前提としています。

 

Hyper-v 拡張可能スイッチのデータパスを経由して移動するパケットトラフィックは、次の方法で拡張機能によって取得されます。

-   拡張機能は、 [*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数が呼び出されたときに、受信データパスからパケットを取得します。 拡張機能は、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出すことによって、受信データパスの基になる拡張機能にパケットを転送します。 フィルターおよび転送拡張機能は、 [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)を呼び出すことによって、受信データパスからパケットを削除することもできます。

-   拡張機能は、 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数が呼び出されたときに、送信データパスからパケットを取得します。 拡張機能は、 [**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を呼び出すことにより、パケットを送信データパスの後続の拡張機能に転送します。 拡張機能のフィルター処理と転送では、 [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)を呼び出すことによって、送信データパスからパケットを削除することもできます。

次のフラグは、 [*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)または[**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)の*sendflags*パラメーターで設定できます。

<a href="" id="ndis-send-flags-switch-single-source"></a>**NDIS\_\_フラグ\_\_単一\_ソースに送信する**  
このフラグが設定されている場合、 [**NET\_BUFFER\_の一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストにあるすべてのパケットは、同じ hyper-v 拡張可能スイッチのソースポートから送信されています。

NDIS が[*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)を呼び出すと、拡張スイッチ拡張インターフェイスが同じソースポートから複数のパケットをグループ化している場合に、このフラグが設定されます。 最適なパフォーマンスを得るために、拡張機能ではこのグループ化を維持し、 [**NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists)を呼び出すときにこのフラグを設定する必要があります。 拡張機能では、一覧内の他のパケットと同じ送信元ポートが使用されている場合に、作成または複製されたパケットを、 [**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストに追加することもできます。

[ **\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストに含まれる各パケットが同じソースポートを使用している場合は、拡張機能によって、 **NDIS\_送信\_完了\_フラグ\_スイッチが設定されることに  \_** 送信要求が完了したときの[**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)の*SENDCOMPLETEFLAGS*パラメーターの単一\_ソースフラグ。

 

<a href="" id="ndis-send-flags-switch-destination-group"></a>**NDIS\_\_フラグを送信し\_\_送信先\_グループに切り替えます**  
このフラグが設定されている場合、[**ネットワーク\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリスト内のすべてのパケットが、同じ拡張可能スイッチの宛先ポートに転送されます。

転送拡張機能では、このフラグを使用して、各パケットの宛先ポートを決定した後、受信データパスで転送する、 [**NET\_BUFFER\_list**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体のリンクリストを指定できます。 このフラグは、パケットを送信データパスの上に転送する前に、拡張可能なスイッチの基になるミニポートエッジによって使用および削除されます。

拡張機能のキャプチャとフィルター処理では、このフラグを使用できません。

転送拡張機能によって、非 NVGRE パケットのパケットの宛先ポートのみが決定さ  **ことに注意**してください。 パケットが NVGRE パケットの場合は、Hyper-v ネットワーク仮想化 (HNV) コンポーネントによってパケットの宛先ポートが決定され、パケットが転送されます。 詳細については、「[ハイブリッド転送](hybrid-forwarding.md)」を参照してください。

 

最適なパフォーマンスを得るには、リンクリスト内のすべてのパケットを同じ宛先ポートに転送する場合は、転送拡張機能でこのフラグを設定する必要があります。 このフラグを設定すると、拡張機能は、リンクリスト内のすべてのパケットが、拡張可能なスイッチ転送コンテキストで同じ宛先ポート要素を持っていることを確認します。

転送拡張機能では、複数の宛先ポートを持つパケットのリンクされたリストに対して、このフラグを設定しない  に**注意**してください。

 

次のフラグは、 [*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)または[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)の*receiveflags*パラメーターで設定できます。

<a href="" id="ndis-receive-flags-switch-single-source"></a>**NDIS\_1 つの\_ソース\_\_の\_フラグを受け取る**  
このフラグが設定されている場合、 [**NET\_BUFFER\_の一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストにあるすべてのパケットは、同じ hyper-v 拡張可能スイッチのソースポートから送信されています。

NDIS が[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)を呼び出すと、拡張可能スイッチが同じ発信元ポートから複数のパケットをグループ化している場合に、このフラグが設定されます。 最適なパフォーマンスを得るために、拡張機能ではこのグループ化を維持し、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すときにこのフラグを設定する必要があります。 また、パケットのソースポートが一覧内の他のパケットと同じである場合は、拡張機能によって、生成または複製されたパケットを、 [**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストに追加する必要があります。

[ **\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストに含まれる各パケットで同じソースポートが使用されている場合は、拡張機能によって**NDIS\_返される\_フラグ\_スイッチ\_SINGLE\_を設定する必要があり  ** 受信要求が完了したときの[*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)の*RETURNFLAGS*パラメーターの SOURCE フラグ。 拡張機能は、 [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)を呼び出して発信または複製されなかったパケットを返す場合、 *returnflags*パラメーターにこのフラグを設定する必要があります。

 

<a href="" id="ndis-receive-flags-switch-destination-group"></a>**NDIS\_\_フラグを受信し\_\_送信先\_グループに切り替えます**  
このフラグが設定されている場合、[**ネットワーク\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリスト内のすべてのパケットが、同じ拡張可能スイッチの宛先ポートに転送されます。

NDIS が[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)を呼び出すと、拡張可能スイッチが同じ宛先ポートを持つ複数のパケットをグループ化している場合に、このフラグが設定されます。 最適なパフォーマンスを得るために、拡張機能ではこのグループ化を維持し、 [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)を呼び出すときにこのフラグを設定する必要があります。 また、パケットの宛先ポートが一覧内の他のパケットと同じである場合は、拡張機能によって、生成または複製されたパケットを、 [**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造のリンクリストに追加する必要があります。

**注**  拡張機能が[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)を呼び出す場合は、 *receiveflags*パラメーターで**NDIS\_RECEIVE\_FLAGS\_RESOURCES**フラグを設定しないようにする必要があります。 拡張可能スイッチインターフェイスは、このフラグを無視し、 [*Filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)を呼び出すことによって受信の通知を完了します。

 

 

 





