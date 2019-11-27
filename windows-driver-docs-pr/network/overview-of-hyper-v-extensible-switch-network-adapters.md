---
title: Hyper-V 拡張可能スイッチ ネットワーク アダプターの概要
description: Hyper-V 拡張可能スイッチ ネットワーク アダプターの概要
ms.assetid: 61403FDE-90BF-4D0A-83E1-5AF8ADBD37A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab83f981cbcbaea6e437d848d7eeca96613cf2ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843745"
---
# <a name="overview-of-hyper-v-extensible-switch-network-adapters"></a>Hyper-V 拡張可能スイッチ ネットワーク アダプターの概要


Hyper-v 拡張可能スイッチは、さまざまな種類の仮想ネットワークアダプターまたは物理ネットワークアダプターからの接続をサポートします。 これらの種類のネットワークアダプターへの接続は、拡張可能なスイッチポートを介して行われます。 ポートは、仮想ネットワークアダプターの接続が確立される前に作成され、ネットワークアダプターの接続が切断された後に削除されます。

たとえば、Hyper-v の子パーティションが開始されると、仮想マシン (VM) ネットワークアダプターがゲストオペレーティングシステム内で公開される前に、拡張可能なスイッチインターフェイスによってポートが作成されます。 VM ネットワークアダプターが公開され、列挙されると、拡張可能なスイッチインターフェイスによって、VM ネットワークアダプターと拡張可能スイッチポートとの間にネットワーク接続が作成されます。 子パーティションが停止している場合、拡張スイッチインターフェイスはまずネットワーク接続を削除してから、拡張可能なスイッチポートを削除します。

Hyper-v 拡張可能スイッチは、次の種類の仮想ネットワークアダプターからの接続をサポートしています。

<a href="" id="external-network-adapters"></a>外部ネットワークアダプター  
これは、Hyper-v の親パーティションで実行されている管理オペレーティングシステムで公開されている拡張可能なスイッチネットワークアダプターです。 拡張可能な各スイッチは、1つの外部ネットワークアダプター接続のみをサポートします。

外部ネットワークアダプターは、ホスト上で使用可能な物理ネットワークインターフェイスへの接続を提供します。 外部ネットワークアダプターには、Hyper-v の親パーティションとすべての子パーティションからアクセスできます。

この種類のネットワークアダプターの詳細については、「[外部ネットワークアダプター](external-network-adapters.md)」を参照してください。

<a href="" id="internal-network-adapters"></a>内部ネットワークアダプター  
これは、Hyper-v の親パーティションで実行されている管理オペレーティングシステムで公開されている拡張可能なスイッチネットワークアダプターです。 拡張可能な各スイッチは、1つの内部ネットワークアダプター接続のみをサポートします。

内部ネットワークアダプターは、管理オペレーティングシステムで実行されるプロセスの拡張可能なスイッチへのアクセスを提供します。 これにより、これらのプロセスが拡張可能スイッチでパケットを送受信できるようになります。

この種類のネットワークアダプターの詳細については、「[内部ネットワークアダプター](internal-network-adapters.md)」を参照してください。

<a href="" id="virtual-machine--vm--network-adapters"></a>仮想マシン (VM) のネットワークアダプター  
これは、Hyper-v 子パーティションで実行されるゲストオペレーティングシステムで公開されている拡張可能なスイッチネットワークアダプターです。

**注**  hyper-v では、子パーティションは VM とも呼ばれます。

 

VM ネットワークアダプターは、次の仮想化の種類をサポートしています。

-   VM ネットワークアダプターは、ネットワークアダプター (*統合ネットワークアダプター*) の統合仮想化である可能性があります。 この場合、VM で実行されるネットワーク仮想サービスクライアント (NetVSC) は、この仮想ネットワークアダプターを公開します。 NetVSC は、VM バス (VMBus) を介して拡張可能なスイッチポートとの間でパケットを転送します。

-   VM ネットワークアダプターは、物理ネットワークアダプター (エミュレートされた*ネットワークアダプター*) のエミュレートされた仮想化である可能性があります。 この場合、VM ネットワークアダプターは Intel ネットワークアダプターを模倣し、ハードウェアエミュレーションを使用して拡張可能なスイッチポートとの間でパケットを転送します。

この種類のネットワークアダプターの詳細については、「[仮想マシンネットワークアダプター](virtual-machine-network-adapters.md)」を参照してください。

拡張可能なスイッチネットワークアダプター接続を作成、更新、削除するには、次の拡張可能なスイッチ OID 要求を使用します。

<a href="" id="oid-switch-nic-create"></a>[OID\_スイッチ\_NIC の作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)  
拡張可能スイッチのプロトコルエッジは oid\_スイッチの OID セット要求を発行し、拡張可能なスイッチポートへのネットワークアダプター接続の作成について拡張可能なスイッチ拡張機能に通知するために、[作成\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)します。 ポートは、oid の oid セット要求を使用して作成されている必要があります[\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)します。

[OID\_スイッチ\_NIC\_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)要求は、新しい拡張可能なスイッチネットワークアダプター接続が確立されていること、および指定されたポートを介してパケットトラフィックが間もなく開始される可能性があることを拡張機能に通知するだけです。

拡張機能は、OID 要求に対して\_受け入れられていないデータ\_ステータス\_返すことによって、作成通知を拒否できます。 たとえば、拡張機能が、ネットワークアダプター接続に使用されるポートで構成されたポリシーを満たすことができない場合、拡張機能は作成通知を拒否する必要があります。

拡張機能が作成通知を受け入れる場合は、OID 要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は、この OID 要求の完了ステータスを監視して、基になる拡張機能が作成通知を拒否したかどうかを判断します。

ネットワークアダプター接続が作成されると、NDIS\_スイッチ\_NIC\_インデックス値に割り当てられます。 このインデックス値は、拡張可能なスイッチポートでのネットワークアダプター接続を識別します。 外部、内部、および VM ネットワークアダプターへの接続には、NDIS\_スイッチ\_NIC\_の\_スイッチのインデックス値が割り当てられます (**既定\_nic\_インデックス**)。\_ 外部ネットワークアダプターにバインドされている各物理ネットワークアダプターまたは仮想ネットワークアダプターには、次の方法で\_NIC\_インデックス値の NDIS\_スイッチが割り当てられます。

-   物理ネットワークアダプターまたは仮想ネットワークアダプターが外部ネットワークアダプターに直接バインドされている場合は、NDIS\_スイッチ\_NIC\_インデックス値が割り当てられます。

-   物理ネットワークアダプターが拡張可能なスイッチチームの一部である場合は、NDIS\_スイッチ\_NIC\_インデックス値が1以上の値に割り当てられます。 拡張可能なスイッチチームは、1つまたは複数の物理ネットワークアダプターのチームが拡張スイッチの外部ネットワークアダプターにバインドされている構成です。

物理ネットワークアダプターを外部ネットワークアダプターにバインドできるさまざまな構成の詳細については、「[物理ネットワークアダプターの構成の種類](types-of-physical-network-adapter-configurations.md)」を参照してください。

NDIS\_スイッチ\_NIC\_インデックス値の詳細については、「[ネットワークアダプターのインデックス値](network-adapter-index-values.md)」を参照してください。

拡張機能がネットワークアダプター接続を介してパケットを生成または転送でき**ない  は**、拡張可能なスイッチのプロトコルエッジが oid セット要求[oid\_スイッチ\_NIC\_接続](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)を発行するまでの間です。

 

<a href="" id="oid-switch-nic-connect"></a>[OID\_スイッチ\_NIC\_接続](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)  
拡張可能スイッチのプロトコルエッジは、oid [\_スイッチ\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)のセット要求を発行して、拡張可能なスイッチネットワークアダプター接続が完全に動作していることを拡張可能なスイッチ拡張機能に通知します。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

OID 要求が NDIS\_STATUS\_SUCCESS によって完了すると、ネットワークアダプター接続と拡張可能スイッチポートは完全に動作します。 ネットワークアダプター接続がこの状態の場合、拡張機能は次の操作を実行できます。

-   ポートのネットワークアダプター接続にパケットトラフィックを生成または転送します。

-   ポートをソースポートとして使用する拡張可能なスイッチ Oid または状態のインジケーターを発行します。

-   参照[*とし*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)て "参照" を呼び出して、ネットワークアダプター接続の参照カウンターを増やします。 参照カウンターの値が0以外の場合、拡張可能なスイッチインターフェイスはネットワークアダプターの接続を停止しません。

<a href="" id="oid-switch-nic-updated"></a>[OID\_スイッチ\_NIC\_更新されました](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-updated)  
拡張可能スイッチのプロトコルエッジは oid\_スイッチの OID セット要求を発行し、拡張スイッチネットワークアダプターのパラメーターが更新されたことを拡張可能なスイッチ拡張に通知するために、\_NIC\_更新されます。 OID は、既に接続されていて、切断プロセスを開始していない Nic に対してのみ発行されます。 これらの実行時構成の変更には、 *NicFriendlyName*、 *MTU*、 *netcfginstanceid*、 *PermanentMacAddress*、 *Vmmacaddress*、 *currentmacaddress*、および*vfassigned*を含めることができます。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

<a href="" id="oid-switch-nic-disconnect"></a>[OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)  
拡張可能スイッチのプロトコルエッジは oid セット要求\_Oid を発行します。これにより、拡張可能なスイッチネットワークアダプター接続が切断されていることを拡張可能なスイッチ拡張機能に通知するために、 [\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)が発生します。 接続が完全に切断された後、拡張可能スイッチのプロトコルエッジは、oid の oid セット要求を発行して[\_スイッチ\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)します。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

拡張機能はこの OID 要求を転送した後、ネットワークアダプター接続が破棄されているポートにパケットを生成したり、転送したりすることができなくなります。 また、拡張機能は、ネットワークアダプター接続に対して、[[*上書き*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)可能] を呼び出すことができなくなります。

<a href="" id="oid-switch-nic-delete"></a>[OID\_スイッチ\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)  
拡張可能スイッチのプロトコルエッジでは、oid セット要求[oid\_スイッチ\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)によって削除されます。拡張可能なスイッチの拡張機能には、拡張スイッチネットワークアダプターの接続が切断され、削除されていることが通知されます。 この OID 要求が発行されるのは、oid\_スイッチの OID セット要求[\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)が既に発行されているネットワーク接続に対してのみです。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要がある  に**注意**してください。 拡張機能は要求を失敗させることはできません。

 

この OID 要求が完了すると、拡張可能スイッチのプロトコルエッジは oid セット要求を\_して、ネットワークアダプター接続に使用されていたポートの削除プロセスを開始するために、 [\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)を行います。

拡張機能は、常にこの OID セット要求を拡張可能なスイッチドライバースタックに転送する必要があります。 拡張機能は要求を失敗させることはできません。

拡張可能なスイッチインターフェイスは、作成されたネットワークアダプター接続ごとに参照カウンターを保持します。 参照カウンターの値が0以外の場合、ネットワークアダプター接続は削除されません。 インターフェイスには、拡張可能なスイッチネットワークアダプター接続の参照カウンターをインクリメントまたはデクリメントするための次のハンドラー関数が用意されています。

<a href="" id="referenceswitchnic"></a>[*上書き/Nic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)  
拡張可能なスイッチ拡張機能は、この関数を呼び出して、ネットワークアダプター接続の参照カウンターをインクリメントします。 参照カウンターに0以外の値が指定されていても、拡張可能スイッチインターフェイスはネットワークアダプター接続を削除しません。

拡張機能では、次の操作を実行する前に、[*上書き*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)ファイルを呼び出す必要があります。

-   拡張可能なスイッチドライバースタック[\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)要求を、基になる外部アダプターに転送する OID\_スイッチに転送します。

-   [**NDIS\_ステータス\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の状態を転送し、基になる外部アダプターから拡張可能なスイッチドライバースタックを示します。

この拡張機能では、oid の OID セット要求を受信した後、ネットワークアダプター接続に対して、その接続に対して[\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)[*を呼び出さ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)ないよう**に  必要**があります。

 

<a href="" id="dereferenceswitchnic"></a>[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)  
拡張可能なスイッチ拡張機能は、この関数を呼び出して、ポートの参照カウンターをデクリメントします。

拡張機能が DereferenceSwitchNic[*を呼び*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)出す場合は、OID\_[](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)要求または[**NDIS\_ステータス\_スイッチ\_nic\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)の表示が完了した後に、 [OID\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)を呼び出す必要があります。

 

 





