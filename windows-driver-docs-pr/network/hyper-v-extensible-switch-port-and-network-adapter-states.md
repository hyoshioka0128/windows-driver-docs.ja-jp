---
title: Hyper-V 拡張可能スイッチ ポートおよびネットワーク アダプターの状態
description: Hyper-V 拡張可能スイッチ ポートおよびネットワーク アダプターの状態
ms.assetid: 1E2075E3-D7CC-4364-ABB2-D5969DB361B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7238a232dc5f58155429587aaaa004bae5b702c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823870"
---
# <a name="hyper-v-extensible-switch-port-and-network-adapter-states"></a>Hyper-V 拡張可能スイッチ ポートおよびネットワーク アダプターの状態


Hyper-v 拡張可能スイッチインターフェイスは、次のコンポーネントの有効期間を管理します。

<a href="" id="hyper-v-extensible-switch-ports"></a>Hyper-v 拡張可能スイッチポート  
拡張可能スイッチへの各ネットワークアダプター接続は、ポートによって表されます。 ポートは、Hyper-v 子パーティションが拡張可能スイッチのインスタンスに接続するように構成されている場合に作成されます。 スイッチの種類によっては、外部および内部ネットワークアダプター接続用のポートも作成されます。 スイッチの種類の詳細については、「 [Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)」を参照してください。

各ポートは、ネットワークインターフェイス接続の構成を保持するために使用されます。 ネットワークインターフェイス接続の構成が削除された場合、または子パーティションが停止した場合、ポートは破棄され、削除されます。

このコンポーネントの詳細については、「 [Hyper-v 拡張可能スイッチポート](hyper-v-extensible-switch-ports.md)」を参照してください。

<a href="" id="hyper-v-extensible-switch-network-adapters"></a>Hyper-v 拡張可能スイッチネットワークアダプター  
これらは、拡張可能なスイッチポートに接続する仮想ネットワークアダプターです。 これらの仮想ネットワークアダプターは、Hyper-v の子パーティションと親パーティション内で公開されます。 これには、子パーティションで公開されている仮想マシン (VM) ネットワークアダプターと、基になる物理ネットワークアダプターとチーミングされた外部ネットワークアダプターが含まれます。

各ネットワークアダプター接続には、対応する拡張可能なスイッチポートが必要です。 ネットワークアダプター接続が起動する前に、ポートが作成されている必要があります。 同様に、ポートを破棄および削除する前に、ネットワークアダプターの接続を削除する必要があります。

**  、** ネットワークアダプター接続を使用しなくても拡張可能なスイッチポートを作成および削除できることがあります。

 

たとえば、Hyper-v の子パーティションが開始されると、VM ネットワークアダプターがゲストオペレーティングシステム内で公開される前に、拡張スイッチインターフェイスによってポートが作成されます。 VM ネットワークアダプターが公開され、列挙されると、拡張可能なスイッチインターフェイスによって、VM ネットワークアダプターと拡張可能スイッチポートとの間にネットワーク接続が作成されます。 子パーティションが停止している場合、拡張スイッチインターフェイスはまずネットワーク接続を削除してから、拡張可能なスイッチポートを削除します。

このコンポーネントの詳細については、「 [Hyper-v 拡張可能スイッチネットワークアダプター](hyper-v-extensible-switch-network-adapters.md)」を参照してください。

拡張可能なスイッチインターフェイスがこれらのコンポーネントの構成を作成、削除、または変更すると、オブジェクト識別子 (OID) セットの要求が拡張可能なスイッチドライバースタックの下位に発行されます。 この操作は、基になる拡張可能なスイッチ拡張機能がコンポーネントとその構成の状態について通知できるようにするために実行されます。 各 OID セット要求は、これらのコンポーネントの状態遷移になります。

拡張機能がバインドされ、拡張可能なスイッチインスタンスで有効になっている場合、そのスイッチの既存のポートとネットワークアダプターの接続構成を検出するために Oid を発行できます。

次の図は、拡張可能なスイッチポートとネットワークアダプター接続コンポーネントのさまざまな状態を示しています。 図には、コンポーネントの状態遷移を発生させる OID セット要求も示されています。

![コンポーネントの状態遷移を発生させる oid セット要求を示すフローチャート](images/vswitchstate.png)

次の一覧では、拡張可能なスイッチポートとネットワークアダプター接続コンポーネントのさまざまな状態について説明します。

<a href="" id="port-not-created"></a>*ポートが作成されていません*  
この状態では、拡張可能スイッチに拡張可能なスイッチポートが存在しません。 以前に作成されたポートを対象とする OID 要求は、ポートがこの状態になった後に発行することはできません。

<a href="" id="port-created"></a>*作成されたポート*  
拡張可能なスイッチインターフェイスが oid の OID セット要求を発行すると[\_\_ポートを作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)、ポートが拡張可能スイッチに作成されます。 この状態では、拡張可能なスイッチインターフェイスと拡張機能は、ポートを対象とする OID 要求を発行できます。

拡張可能なスイッチドライバースタックを介した OID トラフィックの詳細については、「 [Hyper-v 拡張可能スイッチの制御パス](hyper-v-extensible-switch-control-path.md)」を参照してください。

基になる拡張機能によって OID セット要求が失敗し、ポートの作成が拒否さ  場合があることに**注意**してください。 この拡張機能では、状態が\_の OID 要求を完了することによってこれを実行します。データ\_\_は受け入れられません。 この操作を実行すると、拡張可能なスイッチにポートが作成されません。 この手順の詳細については、「 [Hyper-v 拡張可能スイッチポート](hyper-v-extensible-switch-ports.md)」を参照してください。

 

<a href="" id="network-adapter-connection-created"></a>*ネットワークアダプターの接続が作成されました*  
拡張可能なスイッチインターフェイスが oid の OID セット要求を発行すると、 [\_NIC\_作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)、ポートへのネットワークアダプター接続が拡張スイッチに作成されます。 この状態では、拡張可能なスイッチインターフェイスは次の操作を実行できます。

-   ネットワークアダプター接続を対象とする OID 要求を発行します。

-   ネットワークアダプター接続との間でパケットトラフィックを転送します。

また、ポートの破棄と作成シーケンスを経由せずに、新しいアダプターが既存のポートに接続することもできます。

この状態では、拡張機能は、拡張可能なスイッチ拡張機能スタックを介して、これらのパケットと OID 要求を転送する必要があります。 ただし、拡張機能スイッチでは、他のネットワークアダプター接続にパケットや OID 要求を送信したり、リダイレクトしたりすることはできません。

**注**  この状態では、拡張機能は OID 要求を発行したり、ネットワークアダプター接続にパケットトラフィックを発信したりすることはできません。

 

拡張可能なスイッチドライバースタックを介した OID トラフィックの詳細については、「 [Hyper-v 拡張可能スイッチの制御パス](hyper-v-extensible-switch-control-path.md)」を参照してください。

拡張可能なスイッチドライバースタックを介したパケットトラフィックの詳細については、「 [Hyper-v 拡張可能スイッチのデータパス](hyper-v-extensible-switch-data-path.md)」を参照してください。

基になる拡張機能によって OID セット要求が失敗し、ネットワークアダプター接続の作成が拒否される  に**注意**してください。 その場合、接続は拡張可能なスイッチポートで作成されません。 この手順の詳細については、「 [Hyper-v 拡張可能スイッチネットワークアダプター](hyper-v-extensible-switch-network-adapters.md)」を参照してください。

 

<a href="" id="network-adapter-connected"></a>*接続されているネットワークアダプター*  
拡張可能なスイッチインターフェイスが oid の OID セット要求を発行すると、 [\_スイッチ\_NIC\_接続](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)し、ネットワークアダプターが拡張可能なスイッチポートに完全に接続されます。 この状態では、拡張機能は次の操作を実行できるようになります。

-   ネットワークアダプター接続を対象とする OID 要求を発行します。

-   ネットワークアダプター接続にパケットトラフィックを発信します。

-   パケットトラフィックをネットワークアダプター接続にリダイレクトします。 たとえば、拡張機能では、あるネットワークアダプター接続から拡張可能スイッチ上の別の接続にパケットをリダイレクトできます。

    この操作を実行できるのは転送拡張機能のみである  に**注意**してください。 詳細については、「[拡張機能の転送](forwarding-extensions.md)」を参照してください。

     

<a href="" id="network-adapter-disconnected"></a>*ネットワークアダプターが切断されました*  
拡張可能なスイッチインターフェイスが oid の OID セット要求を発行すると、 [\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)すると、ネットワークアダプターは拡張可能なスイッチポートから切断されます。 たとえば、この OID 要求は、VM ネットワークアダプターを公開した子パーティションが停止した場合、または外部ネットワークアダプターが無効になっている場合に発行されます。

この状態では、拡張可能なスイッチ拡張機能は、接続を対象とするパケットまたは OID 要求を開始できなくなります。 また、転送拡張機能はパケットを接続にリダイレクトできなくなります。

接続が切断される前に拡張可能なスイッチインターフェイスによって発行された保留中のパケットおよび OID 要求  、引き続き拡張機能に配信さ**れることが**あります。 ただし、拡張機能では、変更を加えずにパケットと OID 要求を転送する必要があります。

 

<a href="" id="network-adapter-connection-deleted"></a>*ネットワークアダプターの接続が削除されました*  
ネットワークアダプター接続を対象とするすべてのパケットトラフィックと OID 要求が完了すると、拡張可能なスイッチインターフェイスは oid の OID セット要求を\_して[\_\_NIC を削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)し、拡張可能なスイッチから接続を削除します。

この状態では、拡張可能なスイッチインターフェイスは、接続を対象とするパケットまたは OID 要求を発行しなくなります。

<a href="" id="port-tearing-down"></a>*ポートの破棄*  
拡張可能なスイッチインターフェイスが oid の OID セット要求を発行するときに[\_\_ポートの破棄\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)では、拡張可能なスイッチポートが削除される準備として破棄されます。

この状態では、拡張可能なスイッチ拡張機能は、ポートを対象とする OID 要求からは除外されます。

拡張可能なスイッチインターフェイスによって発行された保留中の OID**要求  、** そのポートが破棄プロセスを開始する前に拡張機能に配信される可能性があります。 ただし、拡張機能は、変更を加えずに OID 要求を転送する必要があります。

 

ポートを対象とするすべての保留中の OID 要求が完了すると、拡張可能なスイッチインターフェイスは oid [\_スイッチ\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)の oid セット要求を発行して、削除\_ます。 これにより、ポートが "*ポートが作成されていません*" 状態に移行します。

拡張機能は、拡張可能なスイッチハンドラー関数を呼び出して、ポートまたはネットワークアダプター接続コンポーネントの参照カウンターをインクリメントまたはデクリメントできます。 コンポーネントの参照カウンターが0以外の場合、拡張可能なスイッチインターフェイスはコンポーネントを削除できません。

拡張機能は、参照可能なスイッチポートの参照カウンターをインクリメントまたはデクリメントするために、参照可能な[*Chport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)または[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)を呼び出すことができます。 これらの呼び出しは、ポートが*作成さ*れた状態に到達した後に行うことができます。 ポートが*切断*された後、またはポートが作成されて*いない*状態になった後に、これらの呼び出しを行うことはできません。

この拡張機能で[*は、* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)参照用の "DereferenceSwitchNic" または " [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic) " を呼び出して、拡張可能なスイッチネットワークアダプター接続の参照カウンターを増減できます。 これらの呼び出しは、接続が*ネットワークアダプターの接続*状態に到達した後に行うことができます。 接続が*切断*されたか、*ネットワークアダプターが削除さ*れた状態になった後に、これらの呼び出しを行うことはできません。

次の表では、拡張可能なスイッチポートまたはネットワークアダプター接続コンポーネントの状態に基づいて許可される操作について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネントの状態</th>
<th align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port" data-raw-source="[&lt;em&gt;DereferenceSwitchPort&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)"><em>DereferenceSwitchPort</em></a>を呼び出すことができ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port" data-raw-source="[&lt;em&gt;ReferenceSwitchPort&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)"><em>ますか?</em></a></th>
<th align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic" data-raw-source="[&lt;em&gt;DereferenceSwitchNic&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)"><em>DereferenceSwitchNic</em></a>を呼び出すことができ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic" data-raw-source="[&lt;em&gt;ReferenceSwitchNic&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)"><em>ますか?</em></a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポートが作成されていません</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>作成されたポート</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワークアダプターの接続が作成されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続されているネットワークアダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワークアダプターが切断されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ネットワークアダプターの接続が削除されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポートの破棄</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネントの状態</th>
<th align="left">拡張可能なスイッチからの OID 要求はポートに対して許可されますか?</th>
<th align="left">ポートで許可されている拡張からの OID 要求</th>
<th align="left">ネットワークアダプター接続に対して拡張可能なスイッチから OID 要求を行うことはできますか?</th>
<th align="left">ネットワークアダプター接続が許可されている拡張からの OID 要求</th>
<th align="left">拡張可能スイッチからのパケットトラフィックはネットワークアダプター接続経由で許可されますか?</th>
<th align="left">ネットワークアダプター接続経由で許可される拡張からのパケットトラフィック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポートが作成されていません</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>作成されたポート</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワークアダプターの接続が作成されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続されているネットワークアダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワークアダプターが切断されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ネットワークアダプターの接続が削除されました</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポートの破棄</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

 

 





