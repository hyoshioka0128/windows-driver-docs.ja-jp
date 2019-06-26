---
title: 既定以外の仮想ポートおよび VMQ
description: 既定以外の仮想ポートおよび VMQ
ms.assetid: 5F6F5378-2CA7-491D-953C-6F98B855B51A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721b3b7b508dcb3547f4c4d7e883d7f9a97cb42f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354541"
---
# <a name="nondefault-virtual-ports-and-vmq"></a>既定以外の仮想ポートおよび VMQ


既定の NIC の切り替えは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートするネットワーク アダプターのコンポーネントです。 スイッチに、PCI Express (PCIe) 物理機能 (PF) 既定の仮想ポート (VPort) が常にアタッチします。 スイッチは、PF. に 1 つまたは複数の既定以外拡張をアタッチすることができます。 詳細については、次を参照してください。[仮想ポートを作成する](creating-a-virtual-port.md)します。

仮想化スタックは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。 このスタックは、オブジェクト識別子 (OID) をメソッド要求を発行して拡張を作成します。 [OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。 ただし、スタックの OID メソッド要求を使用するリソースが割り当て済みのアクティブな PCIe 仮想機能 (Vf) の数よりも多くの拡張を作成できます[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。

ネットワーク アダプターで SR-IOV が有効な場合、VMQ のすべての機能を無効にする必要があります。 ただし、既定以外、PF にアタッチされ、VF に関連付けられていないされる拡張では、仮想マシン キュー (VMQ) インターフェイスと同じ機能を提供できます。 次の点では、拡張が VMQ のようなパケット転送のハードウェア アクセラレータを使用したデータ パスを提供する方法について説明します。

-   VMQ は、メディアでの VM へのアクセス制御 (MAC) のハードウェアでフィルター処理の対象を決定します。 これは、仮想化スタックでは、ターゲット VM を決定するオーバーヘッドを回避できます。

    Windows Server 2012 以降では、仮想化スタック受信フィルターの構成、VPort の OID メソッド要求を発行して[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter). この OID 要求に対して、仮想化スタックに渡し、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) MAC アドレスを指定する構造と仮想仮想ネットワーク アダプターに関連付けられている LAN (VLAN) の識別子です。 VMQ と同様に、これを構成できます複数の MAC アドレスと VLAN ID のペア、VPort。 仮想化スタックでは、受信フィルターを設定するターゲット VPort も指定します。

    SR-IOV 対応ネットワーク アダプターのようなハードウェア フィルター処理を実行で指定されたフィルター条件に基づいて、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)要求。 ハードウェアでパケットを受信したときに、VPort のキューの受信、ミニポート ドライバーのアウト オブ バンド (OOB) データでソース VPort 識別子を指定します、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)パケットの構造体。 仮想化スタックは、VPort 識別子に基づいて、ターゲット VM を決定を VM で実行されているネットワーク スタックのパケットを示します。

    同様に、仮想化スタック識別子を指定します、ターゲット VPort の OOB データ、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)送信パケットの構造体。 ドライバーでは、パケットの送信要求を処理する場合は、指定した VPort のハードウェアの送信キューでパケットを配置します。

    使用して、パケットの OOB データから VPort 識別子を取得できます、 [ **NET\_バッファー\_一覧\_受信\_フィルター\_VPORT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)マクロ。

    このプロセスの詳細については、次を参照してください。[仮想ポート経由でのパケット フロー](packet-flow-over-a-virtual-port.md)します。

    受信側のフィルター処理、SR-IOV ネットワーク アダプターの要件の詳細については、次を参照してください。[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)します。

-   VMQ は、割り込みと DPC の同時実行制御を提供します。

    NDIS 6.30 および Windows Server 2012 以降、PF にアタッチされている VPort は、特定の CPU アフィニティを構成できます。 仮想化スタックを VPort の OID メソッド要求を使用して、CPU アフィニティおよび割り込みモデレートのパラメーターを構成する[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)または[OID\_NIC\_スイッチ\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)します。 これにより、仮想化スタックは VMQ の割り込みと DPC の同時実行のような割り込みベースのパラメーターを構成します。

    など、SR-IOV ネットワーク アダプターでは、特定の CPU 関係が構成されている VPort 上のパケットを受信すると、アダプターは、指定した CPU の割り込みを生成します。 ミニポート ドライバーでは、その CPU の NDIS と仮想化スタックにパケットを受信したことを示します。

PF のミニポート ドライバーへの呼び出しのコンテキスト内でその SR-IOV 機能をアドバタイズする[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。 ドライバーの初期化、 [ **NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)その機能と呼び出しを使用した構造[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)その機能を登録します。 詳細については、次を参照してください。 [SR-IOV 機能を決定する](determining-sr-iov-capabilities.md)します。

次のメンバー、 [ **NDIS_NIC_SWITCH_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造が割り当てられている拡張方法に影響します。

-   **MaxNumVPorts**、ネットワーク アダプター上に作成できる拡張の最大数を指定します。

-   **MaxNumVFs**、ネットワーク アダプターに割り当てることができる VFs の最大数を指定します。

NDIS 6.30 以降、ときに、ミニポート ドライバーを初期化します、 [ **NDIS_NIC_SWITCH_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造、NDIS に設定\_NIC\_スイッチ\_CAP\_単一\_VPORT\_プール フラグ、 **NicSwitchCapabilities**メンバー。 このフラグは、既定以外拡張を作成できること、ネットワーク アダプターで VPort プールから引当方法でを指定します。 これにより、使用可能な既定以外の作成と、PF として必要な場合に割り当てられていると VFs を割り当てられている拡張できます。 既定以外の PF に割り当てられている拡張である VMQ インターフェイスが VM のこともでき、ネットワーク アダプターがサポートでは、キューが表示されます。 場合、

場合、NDIS\_NIC\_スイッチ\_CAP\_1 つ\_VPORT\_プール フラグが設定すると、使用可能な既定以外拡張の作成し、PF に割り当てられているされ VFs を割り当てられています。 作成して、PF に割り当てることができます拡張の最大数は同じ値で、ドライバーを報告する、 **MaxNumVPorts**メンバー。 ミニポート ドライバーが VPort、PF. に割り当てられている既定値として使用する 1 つ VPort を予約する必要があります。 その結果、キューの受信、PF に割り当てられているおよび VM に使用できる拡張を既定以外の最大数は (**MaxNumVPorts**– 1)。

> [!NOTE]
> このフラグが設定されている場合 作成と拡張を既定以外の割り当ては VF の割り当てに予約されていません。 その結果、状況は、場所、VF 割り当てることはできません、VPort 使用可能な拡張、プールが使い果たされた場合が発生した可能性があります。 

場合は、NDIS\_NIC\_スイッチ\_CAP\_単一\_VPORT\_プール フラグがセットの作成と割り当ての既定以外の拡張は VF の割り当てのため予約されています。 既定以外を追加作成し、PF に割り当てられているおよび VM 用に使用できる拡張の最大数の受信キューが (**MaxNumVPorts**–**MaxNumVFs**)。

VMQ の詳細については、次を参照してください。[仮想マシン キュー (VMQ)](virtual-machine-queue--vmq-.md)します。
