---
title: Hyper-V 拡張可能スイッチ ポートの概要
description: Hyper-V 拡張可能スイッチ ポートの概要
ms.assetid: FD6B6014-B840-4EC8-96F4-34C08EC303EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09bc9a53e2b1df378b524a17daedd232d0de279
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843742"
---
# <a name="overview-of-hyper-v-extensible-switch-ports"></a>Hyper-V 拡張可能スイッチ ポートの概要


Hyper-v 拡張可能スイッチへの各ネットワーク接続は、ポートによって表されます。 拡張可能なスイッチインターフェイスは、ネットワーク接続が確立される前にポートを作成して構成します。 ネットワーク接続が切断されると、インターフェイスはポートを削除するか、別のネットワーク接続に再利用することができます。

ネットワークインターフェイスを使用して構成されているすべての Hyper-v 子パーティションには、拡張可能スイッチのポートが割り当てられます。 Hyper-v の子パーティションが開始されると、仮想マシン (VM) ネットワークアダプターがゲストオペレーティングシステム内で公開される前に、拡張可能なスイッチインターフェイスによってポートが作成されます。 VM ネットワークアダプターを公開して初期化すると、拡張可能なスイッチインターフェイスによって、VM ネットワークアダプターと拡張可能スイッチポートの間にネットワーク接続が作成されます。 子パーティションが停止している場合、拡張スイッチインターフェイスはまずネットワーク接続を削除してから、拡張可能なスイッチポートを削除します。

拡張可能なスイッチポートが作成されると、一意の識別子と名前を使用して構成されます。 作成した拡張可能なスイッチポートは、ポート経由のパケットトラフィックを管理するためのさまざまな属性を定義するポリシーを使用してプロビジョニングできます。 たとえば、仮想 LAN (VLAN) 属性には標準ポートポリシーを、ポートトラフィックにはアクセス制限を定義できます。 また、独立系ソフトウェアベンダー (Isv) は、個々のポートにプロビジョニングできるカスタムポリシーを定義することもできます。 詳細については、「[ポートポリシー](port-policies.md)」を参照してください。

拡張可能なスイッチポートは、次の種類で構成されます。

<a href="" id="validation-ports"></a>検証ポート  
検証ポートは、ポート設定の検証と検証に使用されます。 これらのポートは一時的なものであり、特定の条件下で作成されます。

たとえば、Hyper-v の子パーティションがネットワークアクセス用に作成または再構成されると、拡張可能なスイッチインターフェイスによって検証ポートが作成されます。 インターフェイスは、このポートを使用して、パーティションの仮想マシン (VM) ネットワークアダプターへのネットワーク接続の設定を確認します。 検証が完了すると、検証ポートが削除され、操作ポートが作成されます。

詳細については、「[検証ポート](validation-ports.md)」を参照してください。

<a href="" id="operational-ports"></a>操作ポート  
操作ポートは、拡張可能なスイッチネットワークアダプター接続をホストするために作成されます。 作成された操作ポートには、ポートの種類が割り当てられます。 このポートの種類は、ポートが作成された後、破棄される前に有効になります。 Hyper-v の子パーティションに割り当てられているポートの場合、操作のポートの種類は、パーティションが実行中で動作している間も有効なままです。

詳細については、「[操作ポート](operational-ports.md)」を参照してください。

拡張可能なスイッチ拡張機能には、次の拡張スイッチオブジェクト識別子 (OID) 要求によってポートの作成、更新、削除が通知されます。

<a href="" id="oid-switch-port-create"></a>[OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)  
拡張可能スイッチのプロトコルエッジは、oid [\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)し、拡張可能なスイッチポートの作成について拡張可能なスイッチ拡張機能に通知します。

拡張機能は、OID 要求に対して\_受け入れられていないデータ\_ステータス\_返すことによって、作成通知を拒否できます。 たとえば、拡張機能が、そのポートで構成されたポリシーを適用するためにリソースを割り当てることができない場合、拡張機能は作成通知を vetoes します。

拡張機能が作成通知を受け入れる場合は、OID 要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は、この OID 要求の完了ステータスを監視して、基になる拡張機能がポート作成通知を拒否したかどうかを判断します。

拡張機能は、ネットワーク接続が作成されるまで、新しく作成されたポートにパケットを転送することはできません。 このプロセスの詳細については、「 [Hyper-v 拡張可能スイッチネットワークアダプター](hyper-v-extensible-switch-network-adapters.md)」を参照してください。

<a href="" id="oid-switch-port-updated"></a>[OID\_スイッチ\_ポート\_更新されました](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)  
拡張可能スイッチのプロトコルエッジは、oid [\_スイッチ\_ポートを更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-updated)して、拡張可能なスイッチポートのパラメーターが更新されていることを拡張可能なスイッチ拡張に通知するように更新\_更新します。 OID は、既に作成されていて、破棄/削除プロセスを開始していないポートに対してのみ発行されます。 現在、 *Portfriendlyname*フィールドのみが、作成後に更新されることがあります。

拡張可能スイッチのプロトコルエッジは、ポートへの以前のネットワーク接続が切断され、ポートに対するすべての OID 要求が完了したときに、この OID 要求を発行します。

この OID 要求は、以前にネットワークアダプター接続がポートに対して行われていなかった場合に発行される  ことに**注意**してください。

 

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

<a href="" id="oid-switch-port-teardown"></a>[OID\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)  
拡張可能スイッチのプロトコルエッジは、拡張スイッチポートが削除されていることを拡張可能なスイッチ拡張に通知するために、oid [\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)の oid セット要求を発行します。 拡張可能スイッチのプロトコルエッジは、ポートへの以前のネットワーク接続が切断され、ポートに対するすべての OID 要求が完了したときに、この OID 要求を発行します。

この OID 要求は、以前にネットワークアダプター接続がポートに対して行われていなかった場合に発行される  ことに**注意**してください。

 

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

拡張機能がこの OID 要求を転送した後、削除されているポートに対する OID 要求を発行できなくなります。

<a href="" id="oid-switch-port-delete"></a>[OID\_スイッチ\_ポートの削除\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)  
拡張可能スイッチのプロトコルエッジは、oid [\_スイッチ\_\_ポートを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)して、拡張可能なスイッチポートが削除されたことを拡張可能なスイッチ拡張に通知します。 拡張可能スイッチのプロトコルエッジは、 [oid\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)要求、およびポートを対象とする oid 要求が完了した後に、この oid 要求を発行します。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

ネットワーク接続用に作成されたすべての拡張可能なスイッチポートには、 **NDIS\_スイッチ\_既定の\_ポート\_ID**を超える識別子が割り当てられます。 **NDIS\_スイッチ\_既定の\_ポート\_ID**識別子は予約されており、次の方法で使用されます。

-   パケットの発信元ポート識別子は、その[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造に関連付けられているパケットの帯域外 (OOB) 転送コンテキストに格納されます。 NDIS\_スイッチの発信元ポート識別子 **\_既定の\_ポート\_ID**は、拡張可能スイッチポートではなく、拡張可能なスイッチ拡張機能からパケットが発信されたことを指定します。 NDIS\_スイッチの発信元ポート識別子を持つパケット **\_既定の\_ポート\_ID**は信頼されており、アクセス制御リスト (acl) やサービスの品質 (QoS) などの拡張可能なスイッチポートポリシーをバイパスします。

    この拡張機能では、パケットが特定のポートから送信されたものとして扱われるようにすることができます。 これにより、そのポートのポリシーをパケットに適用できます。 この拡張機能は、 [*SetNetBufferListSource*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_source)を呼び出してパケットの送信元ポートを変更します。

    ただし、この拡張機能では、パケットの発信元ポート識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に割り当てることが必要になる場合があります。 たとえば、外部ネットワーク上のデバイスに送信される専用の制御パケットに対して、発信元ポートの識別子を**NDIS\_スイッチ\_既定の\_ポート\_ID**に設定することができます。

    転送コンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

-   拡張可能スイッチの外部ネットワークアダプターに発行された OID 要求をカプセル化するために、拡張可能なスイッチインターフェイスによって、 [oid\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)のオブジェクト識別子 (oid) 要求が発行されます。 たとえば、ハードウェアオフロード OID 要求は、拡張可能なスイッチドライバースタックを発行する前に、インターフェイスによってカプセル化されます。

    拡張機能は、拡張可能なスイッチ制御パスで要求を転送するために、カプセル化された OID 要求を発行することもできます。 これにより、拡張機能を使用して、基になる物理ネットワークアダプターの機能を照会または構成できます。

    この OID 要求の **\_oid\_要求**構造の**informationbuffer**メンバーには、 [**ndis\_\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)へのポインターが含まれています。これには、NIC\_OID\_の要求構造が含まれます。 **SourcePortId**メンバーが NDIS に設定されている場合 **\_スイッチ\_既定\_ポート\_ID**で、OID 要求が拡張可能スイッチインターフェイスによって生成されたことを示します。 **DestinationPortId**が NDIS\_に設定されている場合は **\_既定の\_ポート\_ID**に設定されます。これにより、OID 要求が拡張可能スイッチドライバースタックの拡張機能によって処理されることが指定されます。

    OID 要求のコントロールパスの詳細については、「 [Oid 要求の Hyper-v 拡張可能スイッチ制御パス](hyper-v-extensible-switch-control-path-for-oid-requests.md)」を参照してください。

-   Ndis [ **\_status\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の ndis ステータス表示拡張可能スイッチのミニポートエッジによって発行され、拡張可能スイッチの外部ネットワークアダプターから状態の表示をカプセル化します。

    拡張機能は、拡張可能なスイッチコントロールパスを示すために、カプセル化された NDIS 状態のインジケーターを発行することもできます。 これにより、拡張機能は、基になる物理ネットワークアダプターの報告された機能を変更できます。

    [**Ndis\_状態の\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示構造体の**statusbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_状態\_示さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_nic_status_indication)れる構造体が含まれます。 **SourcePortId**メンバーが NDIS に設定されている場合は **\_スイッチ\_既定\_ポート\_ID**である場合は、ステータス表示が拡張可能スイッチインターフェイスによって生成されたことを示します。 **DestinationPortId**が NDIS\_に設定されている場合は **\_既定の\_ポート\_ID**に設定されます。これにより、OID 要求が拡張可能スイッチドライバースタックの拡張機能によって処理されることが指定されます。

    NDIS ステータス表示の制御パスの詳細については、「 [Hyper-v 拡張可能スイッチ制御パス」を](hyper-v-extensible-switch-control-path-for-ndis-status-indications.md)参照してください。

拡張可能なスイッチインターフェイスは、作成された各ポートの参照カウンターを保持します。 参照カウンターの値が0以外の場合、ポートは削除されません。 インターフェイスには、拡張可能なスイッチポートの参照カウンターをインクリメントまたはデクリメントするための次のハンドラー関数が用意されています。

<a href="" id="referenceswitchport"></a>[*上書き/ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
拡張可能なスイッチ拡張機能は、この関数を呼び出して、ポートの参照カウンターをインクリメントします。 参照カウンターに0以外の値が設定されている場合、拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの Oid 要求を発行しません[\_スイッチ\_\_ポートを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)して拡張可能なスイッチポートを削除します。

拡張機能は、ポートがアクティブ状態であることを必要とする操作を実行[*する前に*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)、この拡張機能を呼び出す必要があります。 たとえば、拡張機能では、oid の OID メソッド要求を発行*する前に*、[ [\_ポート]\_プロパティ\_列挙型\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)を呼び出す必要があります。

この拡張機能では、oid の OID セット要求を受信した後、ポート[*に対して*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)、そのポートの[\_ポート\_の破棄\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)**の  を呼び出すことは**できません。

 

<a href="" id="dereferenceswitchport"></a>[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)  
拡張可能なスイッチ拡張機能は、この関数を呼び出して、ポートの参照カウンターをデクリメントします。

この拡張機能は、ポートで実行されている操作が完了した後に[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)を呼び出す必要があります。 たとえば、\_Oid を発行する*前に*、DereferenceSwitchPort を指定した拡張機能を使用して、 [\_ポート\_プロパティ\_列挙型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)要求を発行した場合、拡張機能は oid 要求の後にを呼び出す必要があります。完了.

  NDIS ポートと拡張可能なスイッチポートは異なるオブジェクトである**ことに注意**してください。 拡張可能なスイッチのデータパスを経由して移動するパケットは、常に **\_ndis ポート番号 (既定\_ポート\_番号**) に割り当てられます。 ただし、パケットの発信元と宛先の拡張可能スイッチのポート番号には、 **NDIS\_スイッチ\_既定\_ポート\_ID**以上の値を指定できます。 詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

 

 

 





