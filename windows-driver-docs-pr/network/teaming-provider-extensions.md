---
title: チーミング プロバイダー拡張機能
description: チーミング プロバイダー拡張機能
ms.assetid: 94F73ECD-54D0-4218-B3C4-33DC3BD57ED0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4f4c7173ef582cdc86732051e5f7997eefe7c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379758"
---
# <a name="teaming-provider-extensions"></a>チーミング プロバイダー拡張機能


拡張可能スイッチの外部ネットワーク アダプターは、NDIS マルチプレクサー (マルチプレクサー) の中間ドライバーの仮想ミニポート端にバインドできます。 MUX 中間ドライバー自体は、ホスト上の 1 つまたは複数の物理ネットワーク チームにバインドできます。 この構成と呼ばれる、*拡張可能スイッチ チーム*します。 拡張可能スイッチ チームの詳細については、次を参照してください。[型の物理ネットワーク アダプターの構成](types-of-physical-network-adapter-configurations.md)します。

この構成では、拡張可能スイッチ拡張機能は拡張可能スイッチ チームのすべてのネットワーク アダプターに公開されます。 これにより、転送拡張機能が拡張可能スイッチのドライバー スタックを構成し、チーム内の個々 のネットワーク アダプターの使用を管理するの。 たとえば、拡張機能では、個々 のアダプターに送信されるパケットを転送することによって、over、チーム分散フェールオーバー (LBFO) のソリューション ロードのサポートを提供できます。 このような拡張機能と呼ばれる、*チーミング プロバイダー*します。

次の図には、NDIS 6.40 (Windows Server 2012 R2) と後で外部ネットワーク アダプターにバインドされている、基になる拡張可能スイッチ チームとの間にパケット トラフィックのデータ パスが表示されます。

![ndis 6.40 の外部ネットワーク アダプターにバインドされている、vswitch チームとの間にパケット トラフィック用のデータ パス](images/vswitchteam-ndis640.png)

次の図には、NDIS 6.30 (Windows Server 2012) の外部ネットワーク アダプターにバインドされている、基になる拡張可能スイッチ チームとの間にパケット トラフィックのデータ パスが表示されます。

![ndis 6.30 の外部ネットワーク アダプターにバインドされている、vswitch チームとの間にパケット トラフィック用のデータ パス](images/vswitchteam.png)

プロバイダーをチーミングする転送拡張機能をすべて実行できます。 さらに、プロバイダーのチーミングを以下にします。

-   拡張可能スイッチ チーム内の個々 の物理アダプターに送信パケットを転送します。 この機能は、LBFO 機能のために特に便利です。

-   拡張可能スイッチ チーム内の個々 の物理アダプターに転送標準 NDIS オブジェクト識別子 (OID) を要求します。 この機能は、ハードウェア オフロードのチームでアダプターを構成するために特に便利です。

    たとえば、MUX driver は、全体の拡張可能スイッチ チームの一般的な機能をアドバタイズします。 ただし、チーム化のプロバイダーは、アダプターをチーム内の個々 の機能を照会する OID 要求を発行できます。 次に、チーム化のプロバイダーでは、チーム全体に適用される機能を設定する拡張可能スイッチの外部ネットワーク アダプターに OID 要求を発行できます。

-   拡張可能スイッチ チーム内の個々 の物理アダプターには、プライベートの OID 要求を転送します。 これらのプライベートの OID 要求は、物理ネットワーク アダプターの独立系ハードウェア ベンダー (IHV) によって定義されます。 これにより、IHV 有効または、チーム内の個々 の物理アダプターに専用の属性を無効にして開発されたもチーミング プロバイダーです。

-   拡張可能スイッチ チームからの NDIS 状態インジケーターを変更します。 この機能は、ハードウェアのオフロードの拡張可能スイッチ チームを管理するために特に便利です。

    たとえば、MUX driver は、全体の拡張可能スイッチ チームの一般的な設定で NDIS 状態インジケーターを発行します。 状態の表示が、ハードウェアのオフロードの場合、拡張可能スイッチ チーム ネットワーク アダプターのチーミングのプロバイダーが有効になっている、チーミングのプロバイダーはまず、そのアダプターで現在の機能を照会する OID 要求を発行できます。 次に、チーム化のプロバイダーでは、アダプターの変更がある可能性があるこれらの属性を設定するを示す値のデータを変更できます。

プロバイダーのチーム化、拡張可能スイッチ チームを管理するときにこれらのガイドラインに従う必要があります。

-   チーム化のプロバイダーは、拡張可能スイッチのネットワーク接続が確立された対象のすべての物理ネットワーク アダプターの状態を維持する必要があります。

    拡張可能スイッチのプロトコルのエッジがの独立した OID セット要求を発行する外部ネットワーク アダプターにバインドされているすべての物理ネットワーク アダプターの[OID\_切り替える\_NIC\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)です。 この OID 要求は、基になる物理アダプターにネットワーク接続の作成に関する拡張機能を通知します。

-   物理ネットワーク アダプターへのネットワーク接続が作成されると、外部ネットワーク アダプターが接続されているポートに対して一意である、0 以外のインデックス値が割り当てられます。

    チーム化のプロバイダーは、発行したり、基になる物理ネットワーク アダプターにパケットまたは OID 要求を転送したりする場合、ネットワーク アダプターのインデックス値を指定します。

    詳細については、次を参照してください。[ネットワーク アダプターのインデックス値](network-adapter-index-values.md)します。

-   チーム化のプロバイダーが発行または物理アダプターにパケットを転送は、物理アダプターの接続の 0 以外のネットワーク アダプターのインデックス値を指定する必要があります。

    パケットの帯域外の転送のコンテキストのソースのネットワーク アダプターのインデックス値を決定できるプロバイダーでは、パケットを受信するときに、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 転送コンテキストに関する詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチのデータ パス](hyper-v-extensible-switch-data-path.md)します。

-   物理アダプターに OID 要求の転送を発行するにはチーム化のプロバイダーに OID 要求内でカプセル化、 [ **NDIS\_スイッチ\_NIC\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_oid_request)構造体。 プロバイダーを設定する必要があります、 **DestinationNicIndex**メンバーを物理アダプターの接続の 0 以外のネットワーク アダプターのインデックス値。 プロバイダーの OID セット要求を発行し、 [OID\_スイッチ\_NIC\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)ターゲットの物理アダプターにカプセル化された OID 要求を配信します。

    詳細については、次を参照してください。 [OID 要求を物理ネットワーク アダプターを管理する](managing-oid-requests-to-physical-network-adapters.md)します。

-   チーム化のプロバイダーは、基になる物理アダプターに代わって、NDIS 状態インジケーターを発行できます。 内で示す値をプロバイダーには、カプセル化する必要があります、 [ **NDIS\_スイッチ\_NIC\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_nic_status_indication)構造体。 プロバイダーを設定する必要があります、 **SourceNicIndex**メンバーを物理アダプターの接続の 0 以外のネットワーク アダプターのインデックス値。 プロバイダーの NDIS 状態を示す値を発行し、 [ **NDIS\_状態\_スイッチ\_NIC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)カプセル化された状態を配信するには拡張可能スイッチのドライバー スタックのドライバーの関連を示します。

    詳細については、次を参照してください。[物理ネットワーク アダプターから NDIS 状態インジケーターを管理する](managing-ndis-status-indications-from-physical-network-adapters.md)します。

転送拡張機能の詳細については、次を参照してください。[転送拡張機能](forwarding-extensions.md)します。

MUX ドライバーの詳細については、次を参照してください。 [NDIS MUX 中間ドライバー](ndis-mux-intermediate-drivers.md)します。

 

 





