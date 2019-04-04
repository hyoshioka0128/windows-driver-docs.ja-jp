---
title: HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態
description: HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態
ms.assetid: 1E2075E3-D7CC-4364-ABB2-D5969DB361B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bd220ab2293647821d2615c9831db60bf953363
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528152"
---
# <a name="hyper-v-extensible-switch-port-and-network-adapter-states"></a>HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態


HYPER-V 拡張可能スイッチのインターフェイスは、次のコンポーネントの有効期間を管理します。

<a href="" id="hyper-v-extensible-switch-ports"></a>HYPER-V 拡張可能なスイッチ ポート  
各ネットワーク アダプターの接続、拡張可能スイッチには、ポートで表されます。 HYPER-V 子パーティションが、拡張可能スイッチのインスタンスへの接続に構成されている場合は、ポートが作成されます。 スイッチの種類に応じても外部および内部ネットワーク アダプターの接続用にポートが作成されます。 スイッチの種類の詳細については、[Hyper-v 拡張可能スイッチの概要](overview-of-the-hyper-v-extensible-switch.md)を参照してください。

各ポートは、インターフェイスのネットワーク接続の構成を保持するために使用されます。 インターフェイスのネットワーク接続の構成を解除するか、子パーティションが停止している、ポートが破棄され、削除します。

このコンポーネントの詳細については、[Hyper-v 拡張可能スイッチ ポート](hyper-v-extensible-switch-ports.md)を参照してください。

<a href="" id="hyper-v-extensible-switch-network-adapters"></a>HYPER-V 拡張可能スイッチのネットワーク アダプター  
これらは、拡張可能スイッチ ポートに接続する仮想ネットワーク アダプターです。 これらの仮想ネットワーク アダプターは、HYPER-V 子と親パーティション内で公開されます。 これには、子パーティションと基になる物理ネットワーク アダプターとチーミングは、外部ネットワーク アダプターで公開されている仮想マシン (VM) ネットワーク アダプターが含まれます。

各ネットワーク アダプターの接続には、対応する拡張可能スイッチ ポートが必要です。 ネットワーク アダプターの接続を起動する前に、ポートが作成されている必要があります。 同様に、ネットワーク アダプターの接続をポートを破棄する前に削除し、削除する必要があります。

**注**  状況によっては、拡張可能スイッチのポートを作成および削除しなくても、ネットワーク アダプター接続でした。

 

たとえば、HYPER-V 子パーティションが開始されるは、VM のネットワーク アダプターがゲスト オペレーティング システム内で公開する前に、拡張可能スイッチのインターフェイス ポートは作成します。 VM のネットワーク アダプターが公開され、列挙、拡張可能スイッチのインターフェイスは、VM のネットワーク アダプターと、拡張可能スイッチ ポート間のネットワーク接続を作成します。 子パーティションが停止している場合、拡張可能スイッチのインターフェイスは最初のネットワーク接続を削除し、し、拡張可能スイッチのポートを削除します。

このコンポーネントの詳細については、[Hyper-v 拡張可能スイッチのネットワーク アダプター](hyper-v-extensible-switch-network-adapters.md)を参照してください。

拡張可能スイッチのインターフェイスを作成するには、削除、またはこれらのコンポーネントの構成を変更、ときに、下位の拡張可能スイッチ ドライバー スタック オブジェクト識別子 (OID) のセット要求を発行します。 この操作を実行するは、拡張可能スイッチ拡張機能を基になることができます、コンポーネントとその構成の状態に関する通知を受け取るようにします。 各 OID は、これらのコンポーネントの状態遷移で要求の結果を設定します。

拡張機能では、バインドされ、拡張可能スイッチ インスタンスで有効になっている、ときに、既存のポートとスイッチのネットワーク アダプター接続の構成を検出する Oid を発行できます。

次の図は、拡張可能スイッチのさまざまな状態にポートとネットワーク アダプターの接続コンポーネントを示します。 ダイアグラムには、コンポーネントの状態遷移が発生する OID セット要求も表示されます。

![oid を示すフローチャートは、コンポーネントの状態遷移が発生した要求を設定](images/vswitchstate.png)

次に、拡張可能スイッチのポートとネットワーク アダプターの接続コンポーネントのさまざまな状態を示します。

<a href="" id="port-not-created"></a>*ポートを作成していません。*  
この状態で、拡張可能スイッチのポートは拡張可能スイッチには存在しません。 OID は要求を対象とするポートがこの状態になった後、以前に作成したポートで発行されることはできません。

<a href="" id="port-created"></a>*ポートの作成*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行したとき[OID\_切り替える\_ポート\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598272)、拡張可能スイッチのポートを作成します。 この状態で、拡張可能スイッチのインターフェイスと拡張機能は、ポートをターゲットとする OID 要求を発行できます。

拡張可能スイッチ ドライバー スタックを通じた OID トラフィックに関する詳細については、[Hyper-v 拡張可能スイッチ コントロール パス](hyper-v-extensible-switch-control-path.md)を参照してください。

**注**  基になる拡張機能は OID セットの要求が失敗して、ポートの作成を拒否します。 拡張機能は状態が、OID 要求の完了によって\_データ\_いない\_ACCEPTED です。 これは場合、拡張可能スイッチのポートは作成されません。 この手順の詳細については、[Hyper-v 拡張可能スイッチ ポート](hyper-v-extensible-switch-ports.md)を参照してください。

 

<a href="" id="network-adapter-connection-created"></a>*ネットワーク アダプター接続の作成*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行したとき[OID\_切り替える\_NIC\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598263)、拡張可能スイッチのポートへのネットワーク アダプター接続が作成されます。 この状態で、拡張可能スイッチのインターフェイスは、次の操作を行うことができます。

-   OID の問題は、対象とするネットワーク アダプターの接続を要求します。

-   ネットワーク アダプターの接続との間にパケット トラフィックを転送します。

ポートの破棄を経由せずに既存のポートに接続し、シーケンスを作成する新しいアダプターのこともできます。

この状態で、拡張機能はこれらのパケットと、拡張可能スイッチ拡張機能のスタックを通じて OID 要求を転送する必要があります。 ただし、拡張機能は、発信または拡張可能スイッチの他のネットワーク アダプターの接続をパケットまたは OID 要求をリダイレクトすることはできません。

**注**  この状態で、拡張機能する必要がありますいない OID 要求を発行またはネットワーク アダプターの接続へのトラフィックのパケットを送信します。

 

拡張可能スイッチ ドライバー スタックを通じた OID トラフィックに関する詳細については、[Hyper-v 拡張可能スイッチ コントロール パス](hyper-v-extensible-switch-control-path.md)を参照してください。

拡張可能スイッチ ドライバー スタックを通じたパケット トラフィックに関する詳細については、[Hyper-v 拡張可能スイッチ データ パス](hyper-v-extensible-switch-data-path.md)を参照してください。

**注**  基になる拡張機能は OID セットの要求が失敗して、ネットワーク アダプターの接続の作成を拒否します。 そうである場合、拡張可能スイッチ ポートで、接続は作成されません。 この手順の詳細については、[Hyper-v 拡張可能スイッチのネットワーク アダプター](hyper-v-extensible-switch-network-adapters.md)を参照してください。

 

<a href="" id="network-adapter-connected"></a>*接続されたネットワーク アダプター*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行したとき[OID\_切り替える\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)、ネットワーク アダプターが完全に拡張可能スイッチ ポートに接続されています。 この状態で、拡張機能できるようになりました、次を操作します。

-   OID の問題は、対象とするネットワーク アダプターの接続を要求します。

-   ネットワーク アダプターの接続へのトラフィックのパケットを送信します。

-   ネットワーク アダプターの接続にパケット トラフィックをリダイレクトします。 たとえば、拡張機能は拡張可能スイッチの他の接続を 1 つのネットワーク アダプターの接続からのパケットをリダイレクトできます。

    **注**  この操作を実行できる転送拡張機能のみです。 詳細については、[転送拡張機能](forwarding-extensions.md)を参照してください。

     

<a href="" id="network-adapter-disconnected"></a>*切断されたネットワーク アダプター*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行したとき[OID\_切り替える\_NIC\_切断](https://msdn.microsoft.com/library/windows/hardware/hh598265)、ネットワーク アダプターが拡張可能スイッチ ポートから切断されます。 たとえば、VM のネットワーク アダプターを公開するには、子パーティションが停止しているか、外部ネットワーク アダプターが無効になっているときに、この OID 要求が発行されます。

この状態で、パケットを不要になった開始できるは、拡張可能スイッチの拡張機能または OID を対象とする接続を要求します。 また、転送拡張機能されなくにリダイレクトできますパケット、接続します。

**注**  保留中のパケットと OID、接続が切断される前に、拡張可能スイッチのインターフェイスによって発行された要求される可能性がありますも拡張機能にします。 ただし、拡張する必要があります転送パケットと OID 要求変更を加えずに。

 

<a href="" id="network-adapter-connection-deleted"></a>*ネットワーク アダプター接続の削除*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行するすべてのパケット トラフィックとネットワーク アダプターの接続を対象とする OID 要求が完了したら、 [OID\_切り替える\_NIC\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598264)拡張可能スイッチから、コネクションを削除します。

この状態で、拡張可能スイッチのインターフェイスがパケットを発行しなくまたは OID を対象とする接続を要求します。

<a href="" id="port-tearing-down"></a>*ポートの破棄*  
拡張可能スイッチのインターフェイスがの OID セット要求を発行したとき[OID\_切り替える\_ポート\_破棄](https://msdn.microsoft.com/library/windows/hardware/hh598279)、削除するための準備として、拡張可能スイッチ ポートが破棄されています。

この状態で、拡張可能スイッチ拡張機能開始できるは不要になった OID 要求を対象とするポート。

**注**  ポートは、破棄、プロセスを開始する前に、拡張可能スイッチのインターフェイスによって発行された要求を保留中の OID は、拡張機能にまだ配信可能性があります。 ただし、拡張機能では、変更を加えずに OID 要求を転送する必要があります。

 

拡張可能スイッチのインターフェイスがの OID セット要求を発行する OID 保留中のすべてのポートをターゲットとする要求が完了したら、 [OID\_切り替える\_ポート\_削除](https://msdn.microsoft.com/library/windows/hardware/hh598273)します。 これにより、ポートへの移行、*ポートを作成していない*状態。

拡張機能は、ポートまたはネットワーク アダプターの接続コンポーネントの参照カウンターを増減する拡張可能スイッチ ハンドラー関数を呼び出すことができます。 コンポーネントの参照カウンターが 0 以外の場合、拡張可能スイッチのインターフェイスは、コンポーネントを削除できません。

拡張機能を呼び出すことができます[ *ReferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598295)または[ *DereferenceSwitchPort* ](https://msdn.microsoft.com/library/windows/hardware/hh598142)の参照カウンターを増減する拡張可能スイッチ ポートの場合。 ポートに到達後、これらの呼び出しが行われたことができます、*作成ポート*状態。 ポートに到達後、これらの呼び出しを確立できません必要があります、*解除を行うポート*または*ポートを作成していない*状態。

拡張機能を呼び出すことができます[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)または[ *DereferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598141)の参照カウンターを増減する、拡張可能スイッチのネットワーク アダプターの接続。 接続に達した後、これらの呼び出しが行われたことができます、*接続されたネットワーク アダプター*状態。 接続に達した後、これらの呼び出しを確立できません必要があります、*ネットワーク アダプターが切断されている*または*ネットワーク アダプターの削除*状態。

次の表では、拡張可能スイッチのポートまたはネットワーク アダプターの接続コンポーネントの状態に基づいて許可される操作について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネントの状態</th>
<th align="left">呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/hh598295" data-raw-source="[&lt;em&gt;ReferenceSwitchPort&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598295)"> <em>ReferenceSwitchPort</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/hh598142" data-raw-source="[&lt;em&gt;DereferenceSwitchPort&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598142)"> <em>DereferenceSwitchPort</em> </a>許可しますか?</th>
<th align="left">呼び出す<a href="https://msdn.microsoft.com/library/windows/hardware/hh598294" data-raw-source="[&lt;em&gt;ReferenceSwitchNic&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598294)"> <em>ReferenceSwitchNic</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/hh598141" data-raw-source="[&lt;em&gt;DereferenceSwitchNic&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh598141)"> <em>DereferenceSwitchNic</em> </a>許可しますか?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポートを作成していません。</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ポートの作成</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワーク アダプター接続の作成</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続されたネットワーク アダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>切断されたネットワーク アダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ネットワーク アダプター接続の削除</p></td>
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
<th align="left">ポートの許可されている拡張可能スイッチから OID を要求しますか。</th>
<th align="left">OID は、拡張機能をポートの使用を要求しますか。</th>
<th align="left">ネットワーク アダプター接続の許可されている拡張可能スイッチから OID を要求しますか。</th>
<th align="left">ネットワーク アダプター接続の許可されている拡張機能から OID を要求しますか。</th>
<th align="left">ネットワーク アダプター接続経由で許可されている拡張可能スイッチからのパケット トラフィックですか。</th>
<th align="left">ネットワーク アダプター接続経由で許可されている拡張機能からのパケット トラフィックですか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポートを作成していません。</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ポートの作成</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ネットワーク アダプター接続の作成</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>接続されたネットワーク アダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
</tr>
<tr class="odd">
<td align="left"><p>切断されたネットワーク アダプター</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
</tr>
<tr class="even">
<td align="left"><p>ネットワーク アダプター接続の削除</p></td>
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

 

 

 





