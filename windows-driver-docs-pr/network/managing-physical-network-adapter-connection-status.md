---
title: 物理ネットワーク アダプターの接続状態の管理
description: 物理ネットワーク アダプターの接続状態の管理
ms.assetid: B8C6EB48-59D7-469B-87C8-57E60CB5C5D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34057071a650c24e1e01ffff470263a8ce87982
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382659"
---
# <a name="managing-physical-network-adapter-connection-status"></a>物理ネットワーク アダプターの接続状態の管理


HYPER-V 拡張可能スイッチのアーキテクチャでは、基になる物理メディアにアクセスするため、1 つの外部ネットワーク アダプターへの接続をサポートしています。 外部ネットワーク アダプターは、1 つ以上のさまざまな構成での物理ネットワーク アダプターを基になるにバインドできます。 これらの構成の詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)します。

拡張可能スイッチのインターフェイスには、次の手順を各物理ネットワーク アダプターの接続状態の拡張機能により通知されます。

1.  拡張可能スイッチのプロトコルの端のオブジェクト識別子 (OID) セット要求を発行する[OID\_切り替える\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)です。 この OID 要求では、拡張可能スイッチの外部ネットワーク アダプターへのネットワーク接続の作成に関する拡張可能スイッチの拡張機能を基になるに通知します。

    ネットワーク接続が作成されたときに、NDIS が割り当てられます。\_スイッチ\_NIC\_インデックス値。 このインデックスの値は、拡張可能スイッチ ポートでアダプターのネットワーク接続を識別します。 外部ネットワーク アダプターへのネットワーク接続には、NDIS が割り当てられている\_スイッチ\_NIC\_のインデックス値**NDIS\_スイッチ\_既定\_NIC\_インデックス**します。

2.  拡張可能スイッチのプロトコルのエッジがの独立した OID セット要求を発行する外部ネットワーク アダプターに直接または間接的にバインドされているすべてのネットワーク アダプターの[OID\_切り替える\_NIC\_を作成します](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)。 この OID 要求は、基になるネットワーク アダプターへのネットワーク接続の作成に関する拡張機能を通知します。

    外部ネットワーク アダプターにバインドされている各物理または仮想ネットワーク アダプターには、次のように、識別子が割り当てられます。

    -   1 つの物理アダプターは外部ネットワーク アダプターにバインドする場合、NDIS が割り当てられます。\_スイッチ\_NIC\_1 つのインデックス値。

    -   負荷のネットワーク アダプターのチームを (LBFO) 経由での失敗の分散は、外部ネットワーク アダプターにバインドする場合、NDIS が割り当てられます。\_スイッチ\_NIC\_1 つのインデックス値。

        **注**で、LBFO チーム構成では、LBFO チームをサポートする LBFO プロバイダーの仮想ミニポート edge のみが外部ネットワーク アダプターにバインドすると見なされます。




-   ネットワーク アダプター、拡張可能スイッチ チームは、外部ネットワーク アダプターにバインドする場合、チームの各物理ネットワーク アダプターが割り当てられた一意 NDIS\_切り替える\_NIC\_は 1 つ以上のインデックス値。

    **注**外部ネットワーク アダプターにバインドする拡張可能スイッチ チーム構成では、チーム内のすべての物理ネットワーク アダプターと見なされます。




3.  拡張可能スイッチのプロトコルのエッジの OID セット要求を発行する[OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)外部ネットワーク アダプター。

    **注**この時点で、外部ネットワークへの接続が機能していないとパケット トラフィックに使用することはできません。



4.  拡張可能スイッチのプロトコルのエッジがの独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべてのネットワーク アダプターの[OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)します。 OID の要求の設定後、この OID 要求が発行される[OID\_スイッチ\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)が正常に完了します。

    [OID\_切り替える\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect) OID 要求は、拡張可能スイッチのネットワーク接続が動作して今すぐ、拡張機能に通知します。 プロトコルのエッジが個別の OID を発行の MUX driver 仮想ミニポート edge には、外部ネットワーク アダプターがバインドする場合\_スイッチ\_NIC\_接続を要求します。

    **注**とすぐに、 [OID\_スイッチ\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect) 、NDIS と物理ネットワーク アダプターの要求が発行される\_スイッチ\_NIC\_より大きいインデックス値、またはいずれかに等しい、外部ネットワークへの接続が動作します。 この時点では、トラフィックのパケットを送信または外部のネットワーク経由で受信しました。



5.  拡張可能スイッチのプロトコルのエッジが最初の独立した OID セット要求を発行して外部ネットワーク接続が破棄されている場合[OID\_切り替える\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)すべてのネットワーク外部ネットワーク アダプターにバインドされているアダプターです。 拡張可能スイッチのプロトコルのエッジの個別の OID セット要求を発行してこれらの OID 要求が完了すると、 [OID\_切り替える\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)のすべての物理ネットワーク アダプターを外部ネットワーク アダプターにバインドされます。

    アダプターが切断されているし、拡張可能スイッチに関する問題のプロトコルのエッジを削除後、すべてのネットワーク接続、基になる物理[OID\_切り替える\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)と[OID\_スイッチ\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)要求を切断して外部ネットワーク アダプターの接続を削除します。

詳細については、NDIS\_スイッチ\_NIC\_のインデックス値を参照してください[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。









