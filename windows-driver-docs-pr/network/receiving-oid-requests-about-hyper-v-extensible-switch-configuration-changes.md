---
title: Hyper-v 拡張可能スイッチ構成の受信 OID 要求の変更
description: Hyper-V 拡張可能スイッチ構成変更に関する OID 要求の受信
ms.assetid: 9149BFF3-59B3-4563-A1A1-34FDD115964E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee0675e0e58118dbcd3d77941533d705e37ca5e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842106"
---
# <a name="receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes"></a>Hyper-V 拡張可能スイッチ構成変更に関する OID 要求の受信

拡張可能スイッチインターフェイスは、拡張可能なスイッチオブジェクト識別子 (OID) セット要求を発行することによって、拡張可能なスイッチコンポーネントの構成とポリシーパラメーターの変更について、基になる拡張機能に通知します。 これらの要求は、拡張可能なスイッチのプロトコルエッジによって発行され、拡張可能なスイッチコンポーネントの構成とポリシーパラメーターの変更について、基になる拡張機能に通知します。 これらの OID 要求は拡張可能なスイッチドライバースタックを介して、拡張可能スイッチの基になるミニポートエッジに移動します。

次の図は、NDIS 6.40 (Windows Server 2012 R2) 以降の OID 要求の拡張可能なスイッチ制御パスを示しています。

![ndis 6.40 の vswitch oid 制御パスの図](images/vswitch-oid-controlpath-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の OID 要求の拡張可能なスイッチ制御パスを示しています。

![ndis 6.30 の vswitch oid 制御パスの図](images/vswitch-oid-controlpath.png)

**メモ** 拡張可能なスイッチインターフェイスでは、NDIS フィルタードライバーは*拡張可能なスイッチ拡張機能*と呼ばれ、ドライバースタックは*拡張可能なスイッチドライバースタック*と呼ばれます。 

拡張可能スイッチのプロトコルエッジは、次の種類の通知に対して OID セット要求を発行します。

-   拡張可能スイッチでのポート構成の変更。

    たとえば、プロトコルドライバーは、 [OID\_スイッチ\_\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)を使用して、拡張可能スイッチのポートの作成について、基になる拡張機能に通知します。 同様に、プロトコルドライバーは、ポートの削除について拡張機能に通知するために、 [OID\_スイッチ\_ポートを削除\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)ます。

    この種類の OID 通知の詳細については、「 [Hyper-v 拡張可能スイッチポート](hyper-v-extensible-switch-ports.md)」を参照してください。

-   拡張可能スイッチのポートへのネットワークアダプター接続の変更。

    たとえば、プロトコルドライバーが OID を発行して[\_\_NIC\_接続](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)して、ネットワークアダプターの接続について、基になる拡張機能を拡張可能なスイッチのポートに通知します。 同様に、プロトコルドライバーは、ネットワークアダプターがポートから切断されたことを通知するために、 [\_NIC\_切断を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)して、OID を発行します。

    この種類の OID 通知の詳細については、「 [Hyper-v 拡張可能スイッチネットワークアダプター](hyper-v-extensible-switch-network-adapters.md)」を参照してください。

-   拡張可能なスイッチポートまたはスイッチポリシーの変更。

    たとえば、プロトコルドライバーは[OID\_スイッチ\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)して、拡張可能なスイッチプロパティの追加について、基になる拡張機能に通知します。 同様に、プロトコルドライバーは、ポートのプロパティの削除について拡張機能に通知するために、 [\_ポート\_\_プロパティの\_スイッチの OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)を発行します。

    この種類の OID 通知の詳細については、「 [Hyper-v 拡張可能スイッチポリシーの管理](managing-hyper-v-extensible-switch-extensibility-policies.md)」を参照してください。

    **メモ** 拡張可能スイッチの基になるミニポートエッジによって管理されている既定のポートまたはスイッチポリシーに対する変更は、この拡張機能には通知されません。

-   実行時ポートデータを保存または復元します。

    たとえば、プロトコルドライバーが OID を発行して、 [\_\_NIC を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)します。これにより、基になる拡張機能に通知し、拡張可能スイッチの指定したポートの実行時データを保存するようにします。 これらの Oid は、Hyper-v の状態が保存されるか、別のホストに移行されるときに発行されます。 同様に、プロトコルドライバーは、 [\_NIC\_復元を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)して、拡張スイッチで実行時のポートデータが復元されていることを通知するために、OID を発行します。

    この種類の OID 通知の詳細については、「 [Hyper-v 拡張可能スイッチの実行時データの管理](managing-hyper-v-extensible-switch-run-time-data.md)」を参照してください。

拡張可能なスイッチ拡張機能ミニポートドライバーは、これらの OID 要求を完了する役割を担います。 ただし、一部の拡張スイッチ OID 要求では、基になる拡張機能が OID 要求を失敗させて通知を拒否することができます。 たとえば、拡張可能なスイッチプロトコルドライバーが拡張スイッチで作成される新しいポートについてフィルタードライバーに通知すると、oid [\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)する oid セット要求が発行されます。 基になるフィルター処理または転送拡張機能は、状態が "OID 要求" を完了することによってポートの作成を拒否することがあります。\_データ\_\_受け入れられません。

拡張可能スイッチの拡張機能は、拡張可能なスイッチ OID 要求に対して[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数が呼び出されたときに、次のガイドラインに従う必要があります。

-   拡張機能では、 *OidRequest*パラメーターによって示されるデータを変更することはできません。

-   拡張可能なスイッチ OID 要求によっては、拡張機能によって、状態が\_の OID 要求を完了することができます。データ\_\_は受け入れられません。 これにより、OID 要求が発行された拡張可能なスイッチコンポーネントに対して操作が vetoes されます。

    たとえば、拡張機能によって、 [OID\_スイッチ\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)要求の状態\_データ\_受け入れ\_ないことがあります。 ネットワーク接続の作成先として指定されたポートで構成されたポリシーを満たすことができない場合、ドライバーはこれを行う必要があります。

    拡張機能は、次の Oid に対してこの方法で要求を完了できます。

    -   [OID\_スイッチ\_NIC の作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)

    -   [OID\_スイッチ\_ポート\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)

    -   [OID\_スイッチ\_ポート\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)

    -   [OID\_スイッチ\_ポート\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)

    -   [OID\_スイッチ\_ポート\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)

    -   [OID\_スイッチ\_プロパティ\_追加](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)

    -   [OID\_スイッチ\_プロパティ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)

    -   [OID\_スイッチ\_プロパティ\_更新](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)

-   拡張機能が OID 要求を完了しない場合は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、拡張可能なスイッチドライバースタックに要求を転送する必要があります。

    **メモ** ドライバーが[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出す前に、ドライバーは[**NdisAllocateCloneOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatecloneoidrequest)を呼び出して、 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を割り当て、要求情報を新しい構造体に転送する必要があります。

    拡張機能は、 [*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)関数が呼び出されたときに、OID 要求の完了結果を監視する必要があります。 これにより、拡張可能なスイッチコンポーネントでの操作が正常に完了したか、基になる拡張機能によって拒否されたかを、拡張機能が判断できるようになります。

    OID 要求をフィルター処理して転送する方法の詳細については、「 [NDIS フィルタードライバーでの Oid 要求のフィルター処理](filtering-oid-requests-in-an-ndis-filter-driver.md)」を参照してください。


-   NDIS プロトコルとフィルタードライバーは、ハードウェアオフロードテクノロジに対する OID 要求を基になる物理ネットワークアダプターに発行できます。 これには、仮想マシンキュー (VMQ)、インターネットプロトコルセキュリティ (IPsec)、シングルルート i/o 仮想化 (SR-IOV) などのオフロードテクノロジに対する OID 要求が含まれます。

    これらの OID 要求が拡張可能スイッチインターフェイスに到着すると、 [**NDIS\_スイッチ\_NIC\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)の内部で oid 要求がカプセル化されます。 次に、拡張可能スイッチのプロトコルエッジが、この構造体を含む[NIC\_要求\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)の oid 要求を発行します。

-   拡張可能なスイッチ転送拡張機能を使用すると、外部ネットワークアダプターにバインドされている1つ以上の物理アダプターで、NDIS ハードウェアオフロードテクノロジをサポートできます。 この構成では、拡張可能スイッチの外部ネットワークアダプターが NDIS マルチプレクサー (MUX) 中間ドライバーの仮想ミニポートエッジにバインドされます。 MUX 中間ドライバーは、ホスト上の1つまたは複数の物理ネットワークのチームにバインドされています。 この構成は、*拡張可能なスイッチチーム*と呼ばれています。 拡張可能なスイッチチームの詳細については、「[物理ネットワークアダプターの構成の種類](types-of-physical-network-adapter-configurations.md)」を参照してください。

    この構成では、拡張可能なスイッチ拡張機能がチーム内のすべてのネットワークアダプターに公開されます。 これにより、拡張可能なスイッチドライバースタックの転送拡張機能が、チーム内の個々のネットワークアダプターの構成と使用を管理できるようになります。 たとえば、拡張機能は、送信パケットを個々のアダプターに転送することによって、チームで負荷分散フェールオーバー (LBFO) ソリューションのサポートを提供できます。 このような拡張機能は、*チーミングプロバイダー*と呼ばれます。 チーミングプロバイダーの詳細については、「[チーミングプロバイダーの拡張機能](teaming-provider-extensions.md)」を参照してください。

    Oid の OID 要求を処理することによって[\_NIC\_要求を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)することにより、チーミングプロバイダーはハードウェアのオフロードのためにアダプターチームの構成に参加できます。 たとえば、拡張機能では、独自の oid 要求 OID\_を生成して、ハードウェアオフロード用のパラメーターを使用して物理アダプターを構成するように\_NIC\_要求できます。

    Oid [\_スイッチ\_\_NIC を要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)する方法の詳細については、「 [Oid 要求を物理ネットワークアダプターに転送](forwarding-oid-requests-to-physical-network-adapters.md)する」を参照してください。

    **メモ** 拡張機能フィルタードライバーは、拡張可能スイッチの外部ネットワークアダプターにバインドされている任意の物理アダプターに対してプライベート Oid の発行を要求する oid [\_スイッチ\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)の oid 要求を生成できます。

**メモ** 拡張可能なスイッチ OID 要求が保留中の間は、 [**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter)を使用したスタックの再起動要求は完了しません。 このため、スタックの再開を待機している拡張機能は、実行中の OID 要求を完了する必要があります。

拡張可能なスイッチ OID 要求の制御パスの詳細については、「 [OID 要求の Hyper-v 拡張可能スイッチ制御パス](hyper-v-extensible-switch-control-path-for-oid-requests.md)」を参照してください。









