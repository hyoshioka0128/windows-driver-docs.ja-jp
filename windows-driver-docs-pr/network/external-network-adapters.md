---
title: 外部ネットワーク アダプター
description: 外部ネットワーク アダプター
ms.assetid: 4029437C-97EA-4F21-A3F0-3B29DC650233
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db85c72c9b45c1f6a6a8db3a6981003b0d702c5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353743"
---
# <a name="external-network-adapters"></a>外部ネットワーク アダプター


外部ネットワーク アダプターは、HYPER-V 親パーティションで実行されている管理オペレーティング システムで公開されます。 外部ネットワーク アダプターでは、HYPER-V の外部ネットワークへの接続を提供します。 このネットワークは、ホストの物理ネットワーク インターフェイスにパケット トラフィックを転送します。

外部のネットワークは、HYPER-V 親パーティションと拡張可能スイッチに接続されているすべての子パーティションによってアクセスされます。 拡張可能スイッチの各インスタンスは、複数の外部のネットワーク アダプターの接続をサポートします。

外部ネットワーク アダプターは、基になる物理ネットワーク アダプター、ホスト上の仮想表現です。 外部ネットワーク アダプターでは、パケット、オブジェクト識別子 (Oid) の要求、および 1 つ以上の物理ネットワーク アダプターを基になるとの間の NDIS 状態インジケーターを転送します。

内部的には、外部ネットワーク アダプターは、基になる物理ネットワーク アダプターのさまざまな構成にバインドします。 これらの構成は、1 つまたは複数の物理ネットワーク アダプターを介して外部ネットワーク インターフェイスへのアクセスを提供します。 これらの物理アダプター構成の詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)します。

外部ネットワーク アダプターの接続を提供する拡張可能スイッチを構成する場合、次の手順は、スイッチが開始されると発生します。

1.  拡張可能スイッチのプロトコルの端のオブジェクト識別子 (OID) セット要求を発行する[OID\_切り替える\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、外部ネットワーク アダプター用ポートを作成することを基になる拡張可能スイッチ拡張機能に通知します。

2.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、以前に作成されているポートの外部ネットワーク アダプターのネットワーク接続が作成されていることを基になる拡張可能スイッチ拡張機能に通知します。

3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、外部ネットワーク アダプターのネットワーク接続が接続されていると運用面である、基になる拡張可能スイッチ拡張機能を通知します。 この時点では、拡張機能できます検査、挿入、および外部ネットワーク アダプターに接続されているポートにパケットを転送します。

次の手順は、外部ネットワーク アダプターに接続している拡張可能スイッチが停止しているときに発生します。

1.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)拡張可能スイッチのドライバー スタックがダウンします。 この OID 要求は、基になる外部ネットワーク アダプターへの接続が破棄されている拡張可能スイッチ拡張機能を通知します。

2.  拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行するすべてのパケット トラフィックとネットワーク接続を対象とする OID 要求が完了したら、 [OID\_切り替える\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)下位の拡張可能スイッチ ドライバー スタック。 この OID 要求は、こと外部ネットワーク アダプターへの接続が適切に破棄され削除の基になる拡張可能スイッチ拡張機能を通知します。

3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、基になる外部ネットワーク アダプターの接続に使用されたポートが破棄されている拡張可能スイッチ拡張機能を通知します。

4.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、外部ネットワーク アダプターの接続に使用されたポートを破棄して削除されたことに、基になる拡張可能スイッチ拡張機能を通知します。

 

 





