---
title: Hyper-V 拡張可能スイッチ ポートの概要
description: Hyper-V 拡張可能スイッチ ポートの概要
ms.assetid: FD6B6014-B840-4EC8-96F4-34C08EC303EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ff01d32f99f523035d60dad4cf15d3e7ed6d818
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385720"
---
# <a name="overview-of-hyper-v-extensible-switch-ports"></a>Hyper-V 拡張可能スイッチ ポートの概要


HYPER-V 拡張可能スイッチには、各ネットワーク接続はポートによって表されます。 拡張可能スイッチのインターフェイスは、作成し、ネットワーク接続が行われる前に、ポートを構成します。 ネットワーク接続が切断した後、インターフェイスがポートを削除または別のネットワーク接続の再利用可能性があります。

ネットワーク インターフェイスで構成されているすべての HYPER-V 子パーティションには、拡張可能スイッチのポートが割り当てられます。 HYPER-V 子パーティションが起動したら、仮想マシン (VM) ネットワーク アダプターがゲスト オペレーティング システム内で公開する前に、拡張可能スイッチのインターフェイス ポートを作成します。 VM のネットワーク アダプターが公開され、初期化、拡張可能スイッチのインターフェイスは、VM のネットワーク アダプターと、拡張可能スイッチ ポート間のネットワーク接続を作成します。 子パーティションが停止している場合、拡張可能スイッチのインターフェイスは最初のネットワーク接続を削除し、し、拡張可能スイッチのポートを削除します。

拡張可能スイッチ ポートが作成されると、一意の識別子および名前で構成されます。 作成されたら、ポート経由でトラフィックのパケットの管理のさまざまな属性を定義するポリシー、拡張可能スイッチのポートをプロビジョニングできます。 たとえば、仮想 LAN (VLAN) の属性とポートのトラフィックに関するアクセス制限の標準ポート ポリシーを定義できます。 さらに、独立系ソフトウェア ベンダー (Isv) は、個々 のポートを使用してプロビジョニングできるカスタム ポリシーを定義できます。 詳細については、次を参照してください。[ポート ポリシー](port-policies.md)します。

拡張可能スイッチのポートは、次の種類で構成されます。

<a href="" id="validation-ports"></a>検証のポート  
検証のポートは、ポート設定を検証および確認に使用されます。 これらのポートは一時的なものと、特定の条件下に作成されます。

たとえば、HYPER-V 子パーティションを作成またはネットワーク アクセスを再構成するときに、拡張可能スイッチのインターフェイスは検証ポートを作成します。 インターフェイスは、パーティションの仮想マシン (VM) ネットワーク アダプターへのネットワーク接続の設定を確認するのに、このポートを使用します。 検証が完了した後は、検証のポートが削除され、運用上のポートが作成されます。

詳細については、次を参照してください。[検証ポート](validation-ports.md)します。

<a href="" id="operational-ports"></a>運用上のポート  
拡張可能スイッチ ネットワーク アダプター接続をホストする運用上のポートが作成されます。 運用上のポートが作成されると、ポートの種類が割り当てられます。 破棄する前に、ポートを作成した後、このポートの種類は有効では。 運用上のポートの種類は HYPER-V 子パーティションに割り当てられているポートについては、パーティションが実行され、運用中で有効になります。

詳細については、次を参照してください。[操作ポート](operational-ports.md)します。

拡張可能スイッチの拡張機能は、ポートの作成、更新および拡張可能スイッチ オブジェクトの識別子 (OID) 要求を次の削除の通知されます。

<a href="" id="oid-switch-port-create"></a>[OID\_スイッチ\_ポート\_を作成します。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)に拡張可能スイッチのポートの作成に関する拡張可能スイッチの拡張機能を通知します。

拡張機能は、状態を返すことによって作成の通知を拒否できます\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、その構成済みポリシー、ポートを強制するリソースを割り当てることができません、拡張機能は作成の通知を vetoes します。

場合は、拡張機能は、作成の通知を受け取る、拡張可能スイッチのドライバー スタック ダウン OID 要求を転送する必要があります。 拡張機能は、基になる拡張機能がポートの作成の通知を拒否するかどうかを判断するには、この OID 要求の完了ステータスを監視します。

拡張機能は、ネットワーク接続が作成されるまで、新しく作成したポートにパケットを転送できません。 このプロセスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのネットワーク アダプター](hyper-v-extensible-switch-network-adapters.md)します。

<a href="" id="oid-switch-port-updated"></a>[OID\_スイッチ\_ポート\_更新日](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_UPDATED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)に拡張可能スイッチ ポートのパラメーターは、拡張可能スイッチの拡張機能を通知するには更新されています。 OID は、既に作成されているし、まだ破棄/削除プロセスを開始していないポートにのみ発行されます。 現在は、 *PortFriendlyName*フィールドが作成後に更新されるは。

拡張可能スイッチのプロトコルのエッジは、ポートには、前のネットワーク接続が破損しているし、ポートへのすべての OID 要求が完了したときに、この OID 要求を発行します。

**注**  ネットワーク アダプターの接続が以前のポートに行われたしない場合、この OID 要求を発行できます。

 

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

<a href="" id="oid-switch-port-teardown"></a>[OID\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)に拡張可能スイッチの拡張機能、拡張可能スイッチ ポートが削除されていることを通知します。 拡張可能スイッチのプロトコルのエッジは、ポートには、前のネットワーク接続が破損しているし、ポートへのすべての OID 要求が完了したときに、この OID 要求を発行します。

**注**  ネットワーク アダプターの接続が以前のポートに行われたしない場合、この OID 要求を発行できます。

 

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

後、拡張機能は、この OID 要求を転送するを削除するポートの OID 要求を発行できなくします。

<a href="" id="oid-switch-port-delete"></a>[OID\_スイッチ\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)に拡張可能スイッチの拡張機能で拡張可能スイッチ ポートが削除されたことを通知します。 拡張可能スイッチのプロトコルのエッジは、発行後にこの OID 要求を発行、 [OID\_切り替える\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)要求とポートをターゲットとする OID 要求が完了します。

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

大きい識別子を割り当てられているネットワーク接続用に作成されたすべての拡張可能スイッチ ポート**NDIS\_切り替える\_既定\_ポート\_ID**します。 **NDIS\_スイッチ\_既定\_ポート\_ID**識別子が予約されているし、次の方法で使用します。

-   ソース ポート、パケットの帯域外 (OOB) のコンテキストを転送にパケットが格納されているが関連付けられている識別子、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 ソース ポート識別子**NDIS\_切り替える\_既定\_ポート\_ID**と、拡張可能スイッチではなく、拡張可能スイッチの拡張機能からパケットが発信されたことを指定します。ポート。 パケットの送信元ポートの識別子を**NDIS\_切り替える\_既定\_ポート\_ID**が信頼されており、アクセス制御リスト (Acl など、拡張可能スイッチ ポートのポリシーをバイパスします。) とサービスの品質 (QoS)。

    拡張機能は、特定のポートから送信されたかのように扱う場合にパケットを必要があります。 これにより、パケットに適用するには、そのポートのポリシーができます。 拡張機能の呼び出し[ *SetNetBufferListSource* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)パケットの発信元ポートを変更します。

    ただし、ある可能性があります、拡張機能にパケットの送信元ポートの識別子を割り当てる必要のある状況**NDIS\_スイッチ\_既定\_ポート\_ID**します。 など、拡張機能に設定するソース ポート識別子**NDIS\_スイッチ\_既定\_ポート\_ID**でデバイスに送信されるパケットの独自のコントロール、外部ネットワークです。

    転送コンテキストに関する詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

-   オブジェクトの識別子 (OID) 要求[OID\_切り替える\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)拡張可能スイッチの外部に発行される OID 要求をカプセル化する拡張可能スイッチのインターフェイスによって発行されますネットワーク アダプター。 たとえば、下位の拡張可能スイッチ ドライバー スタックの発行前に、ハードウェア オフロード OID 要求は、インターフェイスによってカプセル化されます。

    拡張機能は、拡張可能スイッチ コントロール パスに要求を転送するためにカプセル化された OID 要求を発行することもできます。 これにより、クエリまたは基になる物理ネットワーク アダプターの機能を構成するための拡張機能です。

    **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**この OID 要求へのポインターが含まれている構造体、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体。 場合、 **SourcePortId**に設定されているメンバー **NDIS\_スイッチ\_既定\_ポート\_ID**、OID 要求によって開始されたことを指定します、拡張可能スイッチのインターフェイスです。 場合、 **DestinationPortId**に設定されている**NDIS\_スイッチ\_既定\_ポート\_ID**、これは、OID 要求が対象となることを指定します。拡張可能スイッチのドライバー スタックの拡張機能で処理します。

    OID 要求の管理パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのコントロール パスの OID 要求](hyper-v-extensible-switch-control-path-for-oid-requests.md)します。

-   状態インジケーターの NDIS [ **NDIS\_状態\_切り替える\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)に拡張可能スイッチのミニポート edge によって発行されます拡張可能スイッチの外部ネットワーク アダプターからの状態表示をカプセル化します。

    拡張機能を使用して、拡張可能スイッチ コントロール パスの問題を転送するために、カプセル化された NDIS 状態インジケーターを発行することもできます。 これにより、拡張機能を基になる物理ネットワーク アダプターの報告機能を変更できます。

    **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)このを示す値をへのポインターが含まれている構造体[ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)構造体。 場合、 **SourcePortId**に設定されているメンバー **NDIS\_スイッチ\_既定\_ポート\_ID**、これは、状態の表示が開始されたことを指定します。で拡張可能スイッチのインターフェイスです。 場合、 **DestinationPortId**に設定されている**NDIS\_スイッチ\_既定\_ポート\_ID**、これは、OID 要求が対象となることを指定します。拡張可能スイッチのドライバー スタックの拡張機能で処理します。

    NDIS 状態インジケーターのコントロール パスの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのコントロール パス NDIS 状態インジケーターの](hyper-v-extensible-switch-control-path-for-ndis-status-indications.md)します。

拡張可能スイッチのインターフェイスは、作成された各ポートの参照カウンターを保持します。 その参照カウンターがある 0 以外の場合、ポートは削除されません。 インターフェイスは、拡張可能スイッチ ポートの参照カウンター、インクリメントまたはデクリメントの次のハンドラー関数を提供します。

<a href="" id="referenceswitchport"></a>[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)  
拡張可能スイッチ拡張機能は、ポートの参照カウンターをインクリメントするには、この関数を呼び出します。 参照カウンターには、0 以外の値が、拡張可能スイッチのプロトコルのエッジのオブジェクト識別子 (OID) セット要求を発行しません[OID\_切り替える\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)を削除します拡張可能スイッチ ポート。

拡張機能を呼び出す必要があります[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)アクティブな状態にするポートを必要とする任意の操作を実行する前にします。 たとえば、拡張機能を呼び出す必要があります*ReferenceSwitchPort*の OID メソッド要求を発行する前に[OID\_スイッチ\_ポート\_プロパティ\_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum).

**注**  、拡張機能を呼び出してはならない[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port) OID を受信した後、ポートの要求のセットの[OID\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)ポート。

 

<a href="" id="dereferenceswitchport"></a>[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)  
拡張可能スイッチ拡張機能は、ポートの参照カウンターをデクリメントするには、この関数を呼び出します。

拡張機能を呼び出す必要があります[ *DereferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)ポートで実行されている操作が完了後します。 例では、拡張機能が呼び出された場合、 *ReferenceSwitchPort*場合の前に発行された、 [OID\_スイッチ\_ポート\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)要求、拡張機能を呼び出す必要があります*DereferenceSwitchPort* OID 要求が完了した後。

**注**  NDIS ポートとスイッチの拡張可能なポートは、さまざまなオブジェクト。 拡張可能スイッチのデータ パス内を移動するパケットは常の NDIS ポート番号を割り当て**NDIS\_既定\_ポート\_数**します。 ただし、パケットの送信元と送信先拡張可能スイッチのポート番号がの値を指定できます**NDIS\_切り替える\_既定\_ポート\_ID**以上。 詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)します。

 

 

 





