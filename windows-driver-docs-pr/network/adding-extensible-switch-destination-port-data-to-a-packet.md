---
title: パケットへの拡張可能スイッチ宛先ポート データの追加
description: パケットへの拡張可能スイッチ宛先ポート データの追加
ms.assetid: C921D9F8-B6FB-4B53-8CC5-CC941720FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d28f4128b54429938043ae82b885a96c1f61f19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384735"
---
# <a name="adding-extensible-switch-destination-port-data-to-a-packet"></a>パケットへの拡張可能スイッチ宛先ポート データの追加


このトピックでは、転送拡張機能、HYPER-V 拡張可能スイッチでパケットの 1 つまたは複数の宛先ポートへの配信を指定する方法について説明します。 これらの拡張機能は、拡張可能スイッチの外部ネットワーク アダプターにバインドされている個々 の物理ネットワーク アダプターにパケットを転送できます。

**注**だけで、転送拡張機能またはスイッチ自体は、拡張可能スイッチのポートまたは個々 のネットワーク アダプターにパケットを転送できます。



次の図には、NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ ドライバー スタックを通じたパケット トラフィックのデータ パスが表示されます。 どちらの図では、拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィックのデータ パスも表示されます。

![ndis 6.40 の更新された拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィック用のデータ パスを示すフローチャート](images/vswitchteam2-ndis640.png)

次の図では、NDIS 6.30 (Windows Server 2012) の拡張可能スイッチ ドライバー スタックを通じたパケット トラフィックのデータ パスが表示されます。

![拡張可能スイッチ ポートに接続されているネットワーク アダプターとの間にパケット トラフィック用のデータ パスを示すフローチャート](images/vswitchteam2.png)

各拡張可能スイッチの宛先ポートがで指定された、 [ **NDIS\_切り替える\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)内の要素、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 この配列は、の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

転送拡張機能がバインドされ、拡張可能スイッチのドライバー スタックで有効になって場合、は、パケットが、NVGRE パケットでない限り、拡張可能スイッチのイングレス データ パスから取得したすべてのパケットの宛先ポートを判断する責任を負います。 このデータ パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パスの概要](overview-of-the-hyper-v-extensible-switch-data-path.md)します。 NVGRE パケットの詳細については、次を参照してください。[ハイブリッド転送](hybrid-forwarding.md)します。

**注**転送拡張機能をドライバー スタックで有効になっている、またはバインドされていない場合、拡張可能スイッチは、イングレス データのパスから取得するパケットの宛先ポートを決定します。



イングレス データ パス取得したパケットの宛先ポートと判断した場合、転送拡張機能は次のガイドラインに従う必要があります。

-   拡張機能を初期化する必要があります、 [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)内で構造体、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)対象のポートの情報を含む構造体。

    宛先ポートが外部ネットワーク アダプターに接続されていない場合、拡張機能を設定する必要があります、 **NicIndex**のメンバー、 [ **NDIS\_スイッチ\_ポート\_移行先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体を**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

    接続先ポートが拡張可能スイッチの外部ネットワーク アダプターに接続されている場合、拡張機能への送信要求を転送するように、基になる物理ネットワーク アダプターのインデックスを指定できます。 拡張機能は設定によって、 **NicIndex**メンバーを 0 以外の NDIS\_スイッチ\_NIC\_外部ネットワーク アダプターにバインドされている変換先のネットワーク アダプターのインデックス値。

    詳細については、次を参照してください。[物理ネットワーク アダプターにパケットを転送](forwarding-packets-to-physical-network-adapters.md)します。

-   拡張機能は、アクティブなネットワーク アダプターの接続があるこれらのポートに対してのみ、パケットの OOB データに宛先ポートを追加する必要があります。 拡張機能が転送した場合、 [OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)要求、切断されたネットワーク アダプターに関連付けられている接続先ポートを追加する必要があります。

-   パフォーマンスを向上させる、拡張機能はのみパケット配信の有効なポートの送信先を追加する必要があります。 この場合、拡張機能を設定する必要があります、 **IsExcluded**の宛先ポートのメンバー [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体を FALSE にします。

-   802.1 q を保持する前に、パケット内の仮想ローカル エリア ネットワーク (VLAN) のデータに配信されます、ポート、拡張機能セット、 **PreserveVLAN**メンバーを TRUE にします。

    802.1 q を削除する前に、パケット内の仮想ローカル エリア ネットワーク (VLAN) のデータに配信されます、ポート、拡張機能セット、 **PreserveVLAN**メンバーを FALSE にします。

-   802.1 q を保持する前にパケットの優先順位のデータに配信されます、ポート、拡張機能セット、 **PreservePriority**メンバーを TRUE にします。

    802.1 q を削除する前にパケットの優先順位のデータが配信されるポートに、拡張機能セット、 **PreservePriority**メンバーを FALSE にします。

-   転送拡張機能は、パケットの複数の宛先ポートを追加する場合は、次の手順に従う必要があります。

    1.  拡張機能には、パケットの最初にアクセスする[ **NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体を使用して、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロ。 次に、拡張機能、読み取り、 **NumAvailableDestinations**先ポートの配列で使用できる未使用の宛先ポート要素の数を決定するメンバー。 呼び出す必要がありますが、拡張機能では、複数の宛先ポート、配列で使用可能な必要がある場合、 [ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数で追加の宛先ポートの容量を割り当てる、配列。

        拡張機能を呼び出すと[ *GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)、設定、 *NumberOfNewDestinations*パラメーターに追加する新しい変換先のポートの数をパケットです。

        また、拡張機能、設定、 *NetBufferLists*パケットへのポインターにパラメーター [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。

        **注**配列内で使用できる変換先のポートがある場合、拡張機能が呼び出す必要がありますいない[ *GrowNetBufferListDestinations*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)します。

    2.  場合、 [ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数が正常に取得、追加の宛先ポートでのコピー先の配列の末尾に追加されて、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 この構造体へのポインターが返される、*宛先*パラメーター。

        **注**場合、 [ *GrowNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_grow_net_buffer_list_destinations)関数は、宛先ポートの要求の数を割り当てることができません、NDIS を返します\_状態\_リソース。

    3.  拡張機能が新しい送信先ポート要素を指定します、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 拡張機能の初期化として新しい各接続先ポート、 [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体。

        拡張機能の初期化を開始位置として、配列に新しい宛先ポート、 **NumDestinations**オフセット。 **NumDestinations**のメンバーである、 [ **NDIS\_スイッチ\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。

    4.  呼び出す必要がありますが、拡張機能には、宛先ポート要素の追加または変更が終了したら、 [ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)変更をコミットします。

-   拡張機能は、パケットの 1 つの宛先ポートを追加する場合は、次の手順に従う必要があります。

    1.  拡張機能が拡張機能が割り当てたでパケットの宛先ポート情報を初期化します[ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体.

    2.  拡張機能の呼び出し[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)への変更をコミットする、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットの構造体。 拡張機能のアドレスを渡す、 [ **NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造体、*先*パラメーター。

        **注**、拡張機能は呼び出さないでください、 [ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)パケットを 1 つだけの宛先ポートに変更をコミットする関数。

-   転送拡張機能を呼び出すと[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)または[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)をコミットします宛先ポートの変更、拡張可能スイッチのインターフェイスは拡張可能スイッチ ポートの要素で指定されている削除されない、 [ **NDIS\_切り替える\_転送\_先\_配列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_destination_array)構造体。 パケットが送信または受信後は、操作が完了したら、インターフェイスが必要がある場合は、ポートを削除する無料。

    **注**宛先ポートが削除された機能とのみにすることはできません転送拡張機能が転送コンテキストに宛先ポートの変更をコミットした後、 **IsExcluded**の宛先ポートのメンバー [**NDIS\_スイッチ\_ポート\_先**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)構造を変更することができます。 詳細については、次を参照してください。[拡張可能スイッチの宛先ポートへのパケット配送の除外](excluding-packet-delivery-to-extensible-switch-destination-ports.md)します。

-   転送拡張機能のオブジェクト識別子 (OID) のセットの要求の処理を同期する必要があります[OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)の宛先ポートを追加するそのコードで、切断されたネットワーク アダプター。

    場合、転送拡張機能の[ *FilterOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)が呼び出されると、 [OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)要求拡張機能は、次のいずれかで実行できます。

    -   拡張機能が呼び出された場合[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)この OID 要求を転送する必要がありますいない指定する必要がポート切断されたネットワーク アダプターを使用したパケットの宛先ポートとして。

        **注**パケットの宛先ポートのみが切断されたネットワーク アダプターを使用した 1 つである場合は、拡張機能によってパケットが破棄する必要があります。

    -   拡張機能は、NDIS を返すことができます\_状態\_保留要求を非同期的に完了します。 これにより、切断されたネットワーク アダプターを使用したパケットの宛先ポートとしてポートを追加する拡張機能です。 また、拡張機能を呼び出す、 [ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)または[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)完全なパケットの宛先ポートの追加。

        拡張機能は可能性がありますが破棄する前に、ポートに転送する必要があるパケットのようにします。

        **注**、拡張機能は、NDIS を返す場合\_状態\_保留中、呼び出すことができますも[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)とポートの参照カウンターをインクリメントするには切断されたネットワーク アダプター。 ただし、拡張機能は転送できませんまで OID 要求呼び出した後[ *DereferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)ポートの参照カウンターをデクリメントします。



-   宛先ポートの数が 0 の場合は、転送拡張機能を呼び出す必要があります[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)パケットをドロップします。 拡張機能を呼び出す必要がありますも[ *ReportFilteredNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists)に破棄されたパケットの拡張可能スイッチのインターフェイスを通知します。

    **注**転送拡張機能のリンク リストを取得する場合は[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)必要があります、イングレス データ パスから複数のパケットの構造体は、破棄されたパケットのリストを作成します。 これにより、拡張機能を呼び出すことができます[ **NdisMSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete)と[ *ReportFilteredNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists) 1 回だけです。



-   宛先ポートの数が 0 より大きい場合は、転送拡張機能を呼び出す必要があります[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)のミニポート エッジへのイングレス データ パスでパケットを転送するように、拡張可能スイッチ。

    **注**転送拡張機能のリンク リストを取得する場合は[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)必要があります、イングレス データ パスから複数のパケットの構造体は、転送されたパケットのリストを作成します。 これにより、拡張機能を呼び出すことができます[ **NdisFSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)パケットのリストを転送するだけで 1 回です。 さらに、拡張機能は、ポートを 1 つの宛先を持つパケットを転送する個別の一覧を管理する必要があります。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの送信と受信フラグ](hyper-v-extensible-switch-send-and-receive-flags.md)します。