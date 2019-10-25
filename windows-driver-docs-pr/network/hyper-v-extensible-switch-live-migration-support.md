---
title: Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート
description: Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート
ms.assetid: 4AFC9E3F-C9C5-4693-BA8C-BC7122A4055F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39dcc24ec24720d1603d8073edc91642c26950df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823884"
---
# <a name="hyper-v-extensible-switch-live-migration-support"></a>Hyper-V 拡張可能スイッチのライブ マイグレーションのサポート


Hyper-v のライブマイグレーション中に、子パーティションまたは*仮想マシン (VM)* が1つのホストコンピューター (*ソースホスト*) で停止し、別のホストコンピューター (*宛先ホスト*) に移行されます。 ライブマイグレーション中に、次の操作が行われます。

-   ソースホストでライブマイグレーションが開始されると、拡張可能なスイッチインターフェイスは、各ポートとそれに関連付けられているネットワークアダプター接続の実行時データを保存するために、基になる拡張機能を要求します。

    この操作の詳細については、「 [Hyper-v 拡張可能スイッチの保存操作](hyper-v-extensible-switch-save-operations.md)」を参照してください。

-   移行先ホストでライブマイグレーションが完了する前に、拡張可能なスイッチインターフェイスは、各ポートとそれに関連付けられているネットワークアダプター接続の実行時データを復元するために、基になる拡張機能を要求します。

    この操作の詳細については、「 [Hyper-v 拡張可能スイッチの復元操作](hyper-v-extensible-switch-restore-operations.md)」を参照してください。

ライブマイグレーションのセットアップ段階で、移行元ホストは、移行先物理ホストとの TCP 接続を作成します。 Hyper-v は、ソース VM の構成データをこの接続を介して移行先の物理ホストに転送します。 移行先ホストにスケルトン VM がセットアップされ、ターゲット VM にメモリが割り当てられます。 この時点で、Hyper-v は、ソース VM の状態 (メモリページを含む) を宛先 VM に転送します。

拡張スイッチインターフェイスでは、ライブマイグレーション中に、TCP 接続を使用してステップと結果を同期することもできます。 たとえば、移行先ホストで実行されているインターフェイスは、移行された VM に関連付けられているポートとネットワークアダプター接続のソースホストからの実行時データの転送を要求します。

宛先 VM が移行先ホストでオンラインになる前に、拡張可能なスイッチインターフェイスによって次の手順が実行されます。

1.  検証ポートは、オブジェクト識別子 (OID) セットの[oid\_スイッチ\_\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)を使用して作成されます。 ポートが正常に作成された場合、拡張可能なスイッチインターフェイスは、基になる拡張機能によってポートポリシーのプロパティを検証するために、他の OID 要求を発行します。

    拡張機能がポートの作成に失敗した場合、またはいずれかのポリシープロパティを無効にした場合、その移行先ノードとスイッチのライブマイグレーションは続行されません。

    検証ポートとその使用法の詳細については、「[検証ポート](validation-ports.md)」を参照してください。

2.  ポリシーのプロパティの検証が正常に完了すると、検証ポートは、変換先のホストで oid セット要求[oid\_スイッチ\_ポート\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)によって削除されます。 このポートが削除されると、移行先ホストで操作ポートが作成され、その代わりに操作ポートが作成されます。 [**NDIS\_スイッチ\_ポート\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)構造に関連付けられている、 [OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)要求、操作ポートに対して、ポートの作成に使用したものと同じデータが含まれています。ソースホスト。

    操作ポートが正常に作成された場合、ポートポリシーは操作ポートに追加されます。

3.  宛先ホストの操作ポートに設定が正常に適用されている場合は、ソースホストの操作ポートに対して保存操作が実行されます。

4.  保存操作が正常に完了した場合、操作ポートとそのネットワークアダプターの接続は、次の方法でソースホスト上で削除されます。

    1.  ネットワーク接続はまず、oid の OID セット要求を使用して切断されます[\_スイッチ\_NIC\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)します。 この OID 要求が完了すると、ソースホスト上のネットワークアダプターの接続は、oid の oid セット要求を使用して削除されます[\_スイッチ\_NIC\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)します。

    2.  ネットワークアダプターの接続が削除されると、操作ポートは oid [\_スイッチ\_ポート\_破棄](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)によって破棄されます。 この OID 要求が完了した後、操作ポートは oid の oid セット要求を使用して削除されます\_スイッチ\_ポート\_削除します。

5.  ネットワークアダプターの接続は、変換先のホストの操作ポートに対して作成されます。これにより、oid [\_スイッチ\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)の設定要求が作成\_ます。 この OID 要求が正常に完了した場合、関連付けられている操作ポートでネットワークアダプター接続が確立されます。 oid [\_スイッチ\_NIC\_接続](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)します。

    ネットワークアダプター接続が正常に確立されると、操作ポートとネットワークアダプター接続の実行時データがターゲットホストに復元されます。

    この時点で、基になる拡張機能がネットワークアダプター接続でリソースの予約と検証を実行できます。

 

 





