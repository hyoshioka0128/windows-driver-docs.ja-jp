---
title: ネットワーク アダプターの HYPER-V 拡張可能スイッチの概要
description: ネットワーク アダプターの HYPER-V 拡張可能スイッチの概要
ms.assetid: 61403FDE-90BF-4D0A-83E1-5AF8ADBD37A5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19e137888c50a8bba8d7f45dfd9ce7ae8fb98b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529422"
---
# <a name="overview-of-hyper-v-extensible-switch-network-adapters"></a>ネットワーク アダプターの HYPER-V 拡張可能スイッチの概要


HYPER-V 拡張可能スイッチには、さまざまな種類の仮想または物理ネットワーク アダプターからの接続がサポートしています。 これらの種類のネットワーク アダプターへの接続は拡張可能スイッチ ポートを介して行われます。 仮想ネットワーク アダプターの接続が行われ、ネットワーク アダプターの接続の破棄後に削除する前に、ポートが作成されます。

たとえば、HYPER-V 子パーティションが開始されると、仮想マシン (VM) ネットワーク アダプターがゲスト オペレーティング システム内で公開する前に拡張可能スイッチのインターフェイスには、ポートが作成されます。 VM のネットワーク アダプターが公開され、列挙、拡張可能スイッチのインターフェイスは、VM のネットワーク アダプターと、拡張可能スイッチ ポート間のネットワーク接続を作成します。 子パーティションが停止している場合、拡張可能スイッチのインターフェイスは最初のネットワーク接続を削除し、し、拡張可能スイッチのポートを削除します。

HYPER-V 拡張可能スイッチには、次の種類の仮想ネットワーク アダプターからの接続がサポートされています。

<a href="" id="external-network-adapters"></a>外部ネットワーク アダプター  
これは、HYPER-V 親パーティションで実行されている管理オペレーティング システムで公開されているスイッチの拡張可能なネットワーク アダプターです。 各拡張可能スイッチには、1 つだけの外部ネットワーク アダプター接続がサポートしています。

外部ネットワーク アダプターでは、ホストで利用可能な物理ネットワーク インターフェイスへの接続を提供します。 外部ネットワーク アダプターは、HYPER-V 親パーティションとすべての子パーティションでアクセスできます。

この種類のネットワーク アダプターの詳細については、[外部ネットワーク アダプター](external-network-adapters.md)を参照してください。

<a href="" id="internal-network-adapters"></a>内部ネットワーク アダプター  
これは、HYPER-V 親パーティションで実行されている管理オペレーティング システムで公開されているスイッチの拡張可能なネットワーク アダプターです。 各拡張可能スイッチには、1 つだけの内部ネットワーク アダプター接続がサポートしています。

内部ネットワーク アダプターでは、管理オペレーティング システムで実行されるプロセスの拡張可能スイッチへのアクセスを提供します。 これにより、これらのプロセスを拡張可能スイッチ経由でパケットを送受信できます。

この種類のネットワーク アダプターの詳細については、[内部のネットワーク アダプター](internal-network-adapters.md)を参照してください。

<a href="" id="virtual-machine--vm--network-adapters"></a>仮想マシン (VM) ネットワーク アダプター  
これは、HYPER-V 子パーティションで実行されているゲスト オペレーティング システムで公開されているスイッチの拡張可能なネットワーク アダプターです。

**注**  で、HYPER-V 子パーティションは、VM でとも呼ばれます。

 

VM のネットワーク アダプターには、次の仮想化の種類がサポートされています。

-   VM のネットワーク アダプターのネットワーク アダプターの仮想化が代理可能性があります (*統合ネットワーク アダプター*)。 この場合、VM で実行されているネットワークの仮想サービス クライアント (NetVSC) は、この仮想ネットワーク アダプターを公開します。 NetVSC VM バス (VMBus) 経由でと、拡張可能スイッチ ポートのパケットを転送します。

-   VM のネットワーク アダプターの物理ネットワーク アダプターの仮想化がエミュレートされた可能性があります (*エミュレートされたネットワーク アダプター*)。 この場合、VM のネットワーク アダプターでは、Intel のネットワーク アダプターを模倣しと拡張可能スイッチ ポートのパケットを転送するようにハードウェアのエミュレーションを使用します。

この種類のネットワーク アダプターの詳細については、[仮想マシンのネットワーク アダプター](virtual-machine-network-adapters.md)を参照してください。

拡張可能スイッチのネットワーク アダプターの接続の作成、更新、および次の拡張可能スイッチ OID 要求を削除していること。

<a href="" id="oid-switch-nic-create"></a>[OID\_スイッチ\_NIC\_を作成します。](https://msdn.microsoft.com/library/windows/hardware/hh598263)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598263)にネットワーク アダプターの接続の作成に関する拡張可能スイッチの拡張機能を通知するには拡張可能スイッチ ポート。 ポートする必要がありますが以前に作成したの OID セットの要求を通じて[OID\_スイッチ\_ポート\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598272)です。

[OID\_切り替える\_NIC\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598263)要求は、拡張には、新しい拡張可能スイッチのネットワーク アダプターの接続が起動されているされ、そのパケット トラフィックが発生する間もなく開始されますのみに通知します。指定されたポート。

拡張機能は、状態を返すことによって作成の通知を拒否できます\_データ\_いない\_OID 要求に使用できます。 たとえば、拡張機能は、ネットワーク アダプターの接続に使用されるポートで構成されているそのポリシーを満たすことができない、拡張機能は作成の通知を拒否する必要があります。

場合は、拡張機能は、作成の通知を受け取る、拡張可能スイッチのドライバー スタック ダウン OID 要求を転送する必要があります。 拡張機能は、基になる拡張機能の作成の通知が拒否されたかどうかを判断するには、この OID 要求の完了ステータスを監視します。

ネットワーク アダプターの接続が作成されたときに、NDIS が割り当てられます。\_スイッチ\_NIC\_インデックス値。 このインデックスの値は、拡張可能スイッチ ポートでネットワーク アダプターの接続を識別します。 外部、内部への接続と VM のネットワーク アダプターが、NDIS を割り当てられている\_スイッチ\_NIC\_のインデックス値**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。 外部ネットワーク アダプターにバインドされている各物理または仮想ネットワーク アダプターには、NDIS が割り当てられている\_スイッチ\_NIC\_次のようにインデックス値。

-   直接、物理または仮想ネットワーク アダプターは外部ネットワーク アダプターにバインドする場合、NDIS が割り当てられます。\_スイッチ\_NIC\_1 つのインデックス値。

-   NDIS が割り当てられている物理ネットワーク アダプターが、拡張可能スイッチ チームの一部である場合、\_切り替える\_NIC\_は 1 つ以上のインデックス値。 拡張可能スイッチ、チームは、1 つまたは複数の物理ネットワーク アダプターのチームが拡張可能スイッチの外部ネットワーク アダプターにバインドされる構成です。

外部ネットワーク アダプターを物理ネットワーク アダプターのバインドのさまざまな構成に関する詳細については、[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)を参照してください。

詳細については、NDIS\_スイッチ\_NIC\_のインデックス値を参照してください[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。

**注**  、拡張機能の生成または拡張可能スイッチのプロトコルのエッジの OID セット要求を発行するまで、ネットワーク アダプターの接続経由でパケットを転送できません[OID\_切り替える\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)します。

 

<a href="" id="oid-switch-nic-connect"></a>[OID\_スイッチ\_NIC\_接続](https://msdn.microsoft.com/library/windows/hardware/hh598262)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)に拡張可能スイッチの拡張機能を通知する、拡張可能スイッチにネットワーク アダプターがあります。接続が完全に動作します。

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

NDIS を使用して要求が完了した後、OID\_状態\_成功した場合、ネットワーク アダプター接続および拡張可能スイッチ ポートが完全に動作します。 ネットワーク アダプターの接続は、この状態が、拡張機能は、以下を実行できます。

-   生成したり、ポートのネットワーク アダプターの接続にパケット トラフィックを転送します。

-   拡張可能な問題は、Oid または発信元ポートとしてポートを使用して、状態インジケーターを切り替えます。

-   呼び出す[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)ネットワーク アダプターの接続の参照カウンターをインクリメントします。 参照カウンターが 0 以外の値を持つときに、拡張可能スイッチのインターフェイスはネットワーク アダプターの接続を終了できません。

<a href="" id="oid-switch-nic-updated"></a>[OID\_スイッチ\_NIC\_更新日](https://msdn.microsoft.com/library/windows/hardware/hh846216)  
OID の OID セット要求を発行する拡張可能スイッチのプロトコル edge\_切り替える\_NIC\_UPDATED に拡張可能スイッチの拡張機能、拡張可能スイッチのネットワーク アダプターのパラメーターが更新されていることを通知します。 OID は、Nic が接続された既にを切断プロセスを開始していないに対してのみ発行されます。 これらの実行時の構成変更を含めることができます*NicFriendlyName*、 *MTU*、 *NetCfgInstanceId*、 *PermanentMacAddress*、*VMMacAddress*、 *CurrentMacAddress*、および*VFAssigned します。*

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

<a href="" id="oid-switch-nic-disconnect"></a>[OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)に拡張可能スイッチの拡張機能を通知する、拡張可能スイッチにネットワーク アダプターがあります。接続が破棄されています。 拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行したら、接続が完全に破損している、 [OID\_切り替える\_NIC\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598264)します。

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

拡張機能は、この OID 要求を転送する後生成もダウンするネットワーク アダプターの接続が破棄されているポートにパケットを転送できなくできます。 また、拡張機能は呼び出すことができなく[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)のネットワーク アダプターの接続。

<a href="" id="oid-switch-nic-delete"></a>[OID\_スイッチ\_NIC\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598264)  
拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598264)に拡張可能スイッチの拡張機能を通知する、拡張可能スイッチにネットワーク アダプターがあります。接続は破棄され、削除します。 この OID 要求は、OID がの要求を設定する対象のネットワーク接続に対してのみ発行[OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)以前に発行されました。

**注**  拡張機能は拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

 

拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行してこの OID 要求が完了すると、 [OID\_切り替える\_ポート\_破棄](https://msdn.microsoft.com/library/windows/hardware/hh598279)がポートの削除プロセスを開始するにはネットワーク アダプターの接続に使用されます。

拡張機能では、拡張可能スイッチのドライバー スタックをこの OID セット要求を常に転送する必要があります。 拡張機能では、要求が失敗しない必要があります。

拡張可能スイッチのインターフェイスは、作成された各ネットワーク アダプター接続の参照カウンターを保持します。 その参照カウンターがある 0 以外の場合、ネットワーク アダプターの接続は削除されません。 インターフェイスには、次のハンドラー関数がインクリメントまたはデクリメント、拡張可能スイッチのネットワーク アダプター接続の参照カウンターを提供します。

<a href="" id="referenceswitchnic"></a>[*ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)  
拡張可能スイッチ拡張機能は、ネットワーク アダプター接続の参照カウンターをインクリメントするには、この関数を呼び出します。 参照カウンターには、0 以外の値が、拡張可能スイッチのインターフェイスでは、このネットワーク アダプターの接続は削除されません。

拡張機能を呼び出す必要があります[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)次の操作を実行する前に。

-   転送、 [OID\_切り替える\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)を基になる外部アダプターに拡張可能スイッチ ドライバー スタックを要求します。

-   転送、 [ **NDIS\_状態\_切り替える\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)拡張可能スイッチ ドライバー スタック基になるまでの状態の表示外部アダプターです。

**注**  、拡張機能を呼び出してはならない[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294) OID を受信した後、接続の要求の設定、ネットワーク アダプターの[OID\_スイッチ\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)接続にします。

 

<a href="" id="dereferenceswitchnic"></a>[*DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)  
拡張可能スイッチ拡張機能は、ポートの参照カウンターをデクリメントするには、この関数を呼び出します。

拡張機能を呼び出す場合[ *ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)、呼び出す必要があります[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)後、 [OID\_スイッチ\_NIC\_要求](https://msdn.microsoft.com/library/windows/hardware/hh598266)または[ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://msdn.microsoft.com/library/windows/hardware/hh598205)完了を示す値。

 

 





