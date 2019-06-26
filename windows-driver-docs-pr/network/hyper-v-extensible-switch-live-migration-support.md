---
title: Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート
description: Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート
ms.assetid: 4AFC9E3F-C9C5-4693-BA8C-BC7122A4055F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfdc8669d31b71fc53e2f6a7fcfcc3f67f5ed09
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383694"
---
# <a name="hyper-v-extensible-switch-live-migration-support"></a>Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート


子パーティションでは、HYPER-V のライブ マイグレーション中または*仮想マシン (VM)* 、1 つのホスト コンピューターが停止している (*ソース ホスト*) と別のホスト コンピューターに移行 (*宛先ホスト*). ライブ移行中に、次の操作が行われます。

-   ライブ マイグレーションは、ソース ホストの起動時に、拡張可能スイッチのインターフェイスは、各ポートと関連付けられているネットワーク アダプター接続の実行時データを保存する基になる拡張機能を要求します。

    この操作の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの保存操作](hyper-v-extensible-switch-save-operations.md)します。

-   宛先のホストでライブ移行の完了前に拡張可能スイッチのインターフェイスは、各ポートと関連付けられているネットワーク アダプター接続の実行時データを復元する基になる拡張機能を要求します。

    この操作の詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの復元操作](hyper-v-extensible-switch-restore-operations.md)します。

ライブ マイグレーションのセットアップ ステージでは、ソース ホストは、変換先の物理ホストとの TCP 接続を作成します。 HYPER-V では、移行先の物理ホストにこの接続で、ソース VM の構成データを転送します。 スケルトン VM でセットアップされて、宛先ホストと接続先の VM メモリの割り当ています。 この時点では、HYPER-V は、接続先の VM にそのメモリ ページをなど、ソース VM の状態を転送します。

拡張可能スイッチのインターフェイスは、ライブ マイグレーション中に手順と結果を同期するのにもの TCP 接続を使用します。 たとえば、宛先ホストで実行されているインターフェイスは、移行した VM に関連付けられているポートとネットワーク アダプターの接続の発信元ホストからの実行時データの転送を要求します。

変換先を転送先ホスト VM がオンラインにする前に、拡張可能スイッチのインターフェイスは、次の手順を実行します。

1.  オブジェクト識別子 (OID) セット要求を転送先ホストの検証のポートが作成された[OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)です。 ポートが正常に作成された場合、拡張可能スイッチ インターフェイスは、基になる拡張機能によってポート ポリシーのプロパティを確認するには、他の OID 要求を発行します。

    場合は、拡張機能は、ポートの作成に失敗またはライブ マイグレーションが引き続きその移行先ノードのおよびスイッチしていないポリシーのプロパティのいずれかを無効にします。

    検証のポートとその使用法の詳細については、次を参照してください。[検証ポート](validation-ports.md)します。

2.  ポリシーのプロパティの検証が正常に完了したら、検証ポートは削除の OID セット要求を転送先ホスト[OID\_スイッチ\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)します。 このポートが削除されると、運用上のポートは宛先のホストで作成し、運用上のポートがその場所に作成します。 [ **NDIS\_スイッチ\_ポート\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造に関連付けられている、 [OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)運用上のポートの要求には、ソース ホスト上のポートの作成に使用された同じデータが含まれています。

    運用上のポートが正しく作成されている場合、ポートのポリシーは、運用上のポートに追加されます。

3.  設定が移行先ホストで、保存操作ポートに正常に適用されている場合、ソース ホスト上の operational ポートの操作が発行されます。

4.  場合、保存操作が正常に完了、運用上のポートとそのネットワーク アダプター接続次のように、ソース ホスト上に削除されます。

    1.  ネットワーク接続が最初の OID セットの要求から切断されている[OID\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)します。 ソース ホスト上のネットワーク アダプター接続がの OID セットの要求によって削除されますこの OID 要求が完了すると、 [OID\_スイッチ\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)します。

    2.  運用上のポートがの OID セット要求を破棄しているネットワーク アダプターの接続が削除されると、 [OID\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)します。 OID の OID セットの要求によって運用上のポートが削除されますこの OID 要求が完了すると、\_スイッチ\_ポート\_を削除します。

5.  運用のポートの OID セット要求を転送先ホストのネットワーク アダプターの接続が作成された[OID\_スイッチ\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)です。 OID セット要求を使用して、関連付けられている操作ポートのネットワーク アダプターの接続が確立されている場合、この OID 要求が正常に完了すると、 [OID\_スイッチ\_NIC\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)します。

    ネットワーク アダプターの接続が正常に確立されると、運用上のポートおよびネットワーク アダプター接続の実行時のデータは、ターゲット ホストに復元されます。

    この時点では、基になる拡張機能を実行できますリソースの予約と検証のネットワーク アダプターの接続。

 

 





