---
title: 内部ネットワーク アダプター
description: 内部ネットワーク アダプター
ms.assetid: 4E4B0EC9-8E4C-47FC-B608-EC6D18367A79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f5794fd560088a6d5e696abcde45a3c4a50658
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354551"
---
# <a name="internal-network-adapters"></a>内部ネットワーク アダプター


内部ネットワーク アダプターは、HYPER-V 親パーティションで実行されている管理オペレーティング システムで公開されます。 この種類のネットワーク アダプターでは、管理オペレーティング システムで実行されるプロセスの拡張可能スイッチへのアクセスを提供します。 これにより、これらのプロセスを拡張可能スイッチ経由でパケットを送受信できます。

内部ネットワーク アダプターの接続を提供する拡張可能スイッチを構成する場合、次の手順は、スイッチが開始されると発生します。

1.  拡張可能スイッチのプロトコルの端のオブジェクト識別子 (OID) セット要求を発行する[OID\_切り替える\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、内部ネットワーク アダプター用ポートを作成することを基になる拡張可能スイッチ拡張機能に通知します。

2.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、以前に作成されているポートの内部ネットワーク アダプターのネットワーク接続が作成されていることを基になる拡張可能スイッチ拡張機能に通知します。

3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、内部ネットワーク アダプターのネットワーク接続が接続されていると運用面である、基になる拡張可能スイッチ拡張機能を通知します。 この時点では、拡張機能できます検査、挿入、および内部ネットワーク アダプターに接続されているポートにパケットを転送します。

次の手順は、内部ネットワーク アダプターに接続している拡張可能スイッチが停止しているときに発生します。

1.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)拡張可能スイッチのドライバー スタックがダウンします。 この OID 要求は、基になる外部ネットワーク アダプターへの接続が破棄されている拡張可能スイッチ拡張機能を通知します。

2.  拡張可能スイッチのプロトコルのエッジがの OID セット要求を発行するすべてのパケット トラフィックとネットワーク接続を対象とする OID 要求が完了したら、 [OID\_切り替える\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)下位の拡張可能スイッチ ドライバー スタック。 この OID 要求は、こと外部ネットワーク アダプターへの接続が適切に破棄され削除の基になる拡張可能スイッチ拡張機能を通知します。

3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、基になる外部ネットワーク アダプターの接続に使用されたポートが破棄されている拡張可能スイッチ拡張機能を通知します。

4.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)拡張可能スイッチのドライバー スタックのダウンします。 この OID 要求は、内部ネットワーク アダプターの接続に使用されたポートを破棄して削除されたことに、基になる拡張可能スイッチ拡張機能を通知します。

 

 





