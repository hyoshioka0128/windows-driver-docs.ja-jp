---
title: 仮想マシン ネットワーク アダプター
description: 仮想マシン ネットワーク アダプター
ms.assetid: 8A2A708C-AB43-4D9F-A7CB-2AC4438BCD54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aadc38e75eeb8efdb9a97a3606dcf8723f1d1566
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354489"
---
# <a name="virtual-machine-network-adapters"></a>仮想マシン ネットワーク アダプター


仮想マシン (VM) ネットワーク アダプターは、HYPER-V 子パーティションで実行されているゲスト オペレーティング システムで公開されます。

**注**  で、HYPER-V 子パーティションは、VM でとも呼ばれます。

 

VM のネットワーク アダプターには、次の仮想化の種類がサポートされています。

-   VM のネットワーク アダプターのネットワーク アダプターの仮想化が代理可能性があります (*統合ネットワーク アダプター*)。 この場合、VM で実行されているネットワークの仮想サービス クライアント (NetVSC) は、この仮想ネットワーク アダプターを公開します。 NetVSC VM バス (VMBus) 経由でと、拡張可能スイッチ ポートのパケットを転送します。

-   VM のネットワーク アダプターの物理ネットワーク アダプターの仮想化がエミュレートされた可能性があります (*エミュレートされたネットワーク アダプター*)。 この場合、VM のネットワーク アダプターでは、Intel のネットワーク アダプターを模倣しと拡張可能スイッチ ポートのパケットを転送するようにハードウェアのエミュレーションを使用します。

次の図は、VM のネットワーク アダプター間のインターフェイスと、拡張可能なスイッチ NDIS 6.40 (Windows Server 2012 R2) 以降。

![エミュレートされた vm のネットワーク アダプターと ndis 6.40 の拡張可能スイッチ間のインターフェイスを示すフローチャート](images/vswitchvmnic-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の VM のネットワーク アダプターと拡張可能スイッチ間のインターフェイスを示します。

![エミュレートされた vm のネットワーク アダプターと ndis 6.30 の拡張可能スイッチ間のインターフェイスを示すフローチャート](images/vswitchvmnic.png)

次の手順は、ユーザーが、HYPER-V VM を起動するときに発生します。

1.  拡張可能スイッチのプロトコルの端のオブジェクト識別子 (OID) セット要求を発行する[OID\_切り替える\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、VM 用のポートを作成することを基になる拡張可能スイッチ拡張機能に通知します。

2.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、VM のネットワーク アダプターのネットワーク接続が既に作成されている VM のポートの作成されることを基になる拡張可能スイッチ拡張機能に通知します。

3.  拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行するときに、ネットワーク スタックが正常に動作し、VM のネットワーク アダプターにバインドされている、 [OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)ダウン拡張可能スイッチ ドライバー スタックです。 この OID 要求は、VM のネットワーク アダプターのネットワーク接続が接続されていると運用面である、基になる拡張可能スイッチ拡張機能を通知します。 この時点では、拡張機能できます検査、挿入、および VM ネットワーク アダプターに接続されているポートにパケットを転送します。

次の手順は、ユーザーは、HYPER-V VM を停止したときに発生します。

1.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)拡張可能スイッチのドライバー スタックがダウンします。 この OID 要求は、基になる VM のネットワーク アダプターへの接続が破棄されている拡張可能スイッチ拡張機能を通知します。

2.  拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行するすべてのパケット トラフィックとネットワーク接続を対象とする OID 要求が完了したら、 [OID\_切り替える\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)下位の拡張可能スイッチ ドライバー スタック。 この OID 要求は、VM のネットワーク アダプターへの接続がされて適切に破棄を削除、基になる拡張可能スイッチ拡張機能を通知します。

3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、基になる VM のネットワーク アダプターの接続に使用されたポートが破棄されている拡張可能スイッチ拡張機能を通知します。

4.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、VM のポートを破棄して削除されたことに、基になる拡張可能スイッチ拡張機能を通知します。

 

 





