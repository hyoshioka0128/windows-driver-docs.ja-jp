---
title: 既定以外の仮想ポートおよび VMQ
description: 既定以外の仮想ポートおよび VMQ
ms.assetid: 5F6F5378-2CA7-491D-953C-6F98B855B51A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e2f09cfd9d19cb78bac6e7b5d536c128490c1ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842765"
---
# <a name="nondefault-virtual-ports-and-vmq"></a>既定以外の仮想ポートおよび VMQ


既定の NIC スイッチは、シングルルート i/o 仮想化 (SR-IOV) インターフェイスをサポートするネットワークアダプターのコンポーネントです。 スイッチは常に既定の仮想ポート (VPort) を PCI Express (PCIe) 物理機能 (PF) にアタッチします。 スイッチは、1つまたは複数の既定以外の VPorts を PF に接続できます。 詳細については、「[仮想ポートの作成](creating-a-virtual-port.md)」を参照してください。

仮想化スタックは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。 このスタックは、Oid\_NIC\_スイッチのオブジェクト識別子 (OID) メソッド要求を発行して VPorts を作成し[\_\_vports を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。 ただし、スタックでは、Oid による oid メソッド要求[oid\_\_\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)使用してリソースが割り当てられているアクティブな PCIe 仮想関数 (VFs) の数よりも多くの vports を作成できます。

ネットワークアダプターで sr-iov が有効になっている場合は、完全な VMQ 機能を無効にする必要があります。 ただし、PF にアタッチされ、VF に接続されていない既定以外の VPorts は、バーチャルマシンキュー (VMQ) インターフェイスと同じ機能を提供できます。 次の点で、VPorts が VMQ に似たパケット転送用にハードウェアアクセラレータのデータパスを提供する方法について説明します。

-   VMQ は、ハードウェアでメディアアクセス制御 (MAC) フィルタリングを使用してターゲット VM を決定します。 これにより、仮想化スタック内のターゲット VM を決定する際のオーバーヘッドを回避できます。

    Windows Server 2012 以降では、仮想化スタックは、Oid の OID メソッド要求を発行することによって、VPort の受信フィルターを構成[\_フィルター\_設定して、\_フィルターを受信\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 この OID 要求では、仮想化スタックは、仮想ネットワークアダプターに関連付けられている MAC アドレスと仮想 LAN (VLAN) 識別子を指定する、 [ **\_フィルター\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)を渡します。 VMQ と同様に、VPort に複数の MAC アドレスと VLAN ID のペアを構成することができます。 また、仮想化スタックでは、受信フィルターを設定するターゲットの VPort も指定します。

    SR-IOV ネットワークアダプターは、OID によって指定されたフィルター条件に基づいて、同様のハードウェアフィルター処理を実行します。このフィルターの条件は、フィルターの要求[\_フィルター\_設定された OID\_受信\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)です。 パケットが VPort のハードウェア受信キューで受信されると、ミニポートドライバーは、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の帯域外 (OOB) データのソース vport 識別子を指定します。 仮想化スタックは、VPort 識別子に基づいてターゲット VM を決定し、VM で実行されるネットワークスタックへのパケットを示します。

    同様に、仮想化スタックは、送信パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データ内のターゲット vport 識別子を指定します。 ドライバーは、パケットの送信要求を処理するときに、指定された VPort のハードウェア転送キューにパケットを置きます。

    VPort id はパケットの OOB データから取得できます。そのためには、 [**NET\_BUFFER\_LIST を使用して\_FILTER\_VPORT\_ID マクロを受信\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)ます。

    このプロセスの詳細については、「[仮想ポート経由のパケットフロー](packet-flow-over-a-virtual-port.md)」を参照してください。

    SR-IOV ネットワークアダプターの受信フィルター処理の要件の詳細については、「[受信フィルター機能の決定](determining-receive-filtering-capabilities.md)」を参照してください。

-   VMQ は、割り込みと DPC の同時実行を提供します。

    NDIS 6.30 および Windows Server 2012 以降では、特定の CPU アフィニティを持つように PF に接続された VPort を構成できます。 仮想化スタックは、Oid の OID メソッド要求 Oid\_使用して、VPort の CPU アフィニティと割り込みモデレーションのパラメーターを構成します。 [\_スイッチ\_\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)または[oid\_nic\_スイッチを作成\_VPORT\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)。 これにより、仮想化スタックは、割り込みおよび DPC 同時実行のための VMQ と同様の割り込みベースのパラメーターを構成します。

    たとえば、SR-IOV ネットワークアダプターが特定の CPU アフィニティを持つように構成された VPort でパケットを受信する場合、アダプターは、指定された CPU に割り込みを生成します。 ミニポートドライバーは、NDIS に対して受信したパケットとその CPU の仮想化スタックを示します。

PF ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しのコンテキスト内で sr-iov 機能をアドバタイズします。 このドライバーは、その機能を使用して[**NDIS\_SRIOV\_capabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体を初期化し、その機能を登録するために[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出します。 詳細については、「 [Sr-iov 機能の決定](determining-sr-iov-capabilities.md)」を参照してください。

[**NDIS_NIC_SWITCH_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体の次のメンバーは、vports の割り当て方法に影響します。

-   **Maxnumvports**。ネットワークアダプターに作成できる vports の最大数を指定します。

-   **Maxnumvfs**。ネットワークアダプターに割り当てることができる vfs の最大数を指定します。

NDIS 6.30 以降では、ミニポートドライバーによって[**NDIS_NIC_SWITCH_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)構造体が初期化されるときに、NDIS\_NIC\_スイッチ\_CAP\_1 つの\_VPORT\_プールフラグ**を設定できます。NicSwitchCapabilities**メンバー。 このフラグは、既定以外の VPorts をネットワークアダプターの Vports プールから予約されていない方法で作成できることを指定します。 これにより、使用可能な既定以外の VPorts を作成し、必要に応じて PF と割り当てられた VFs に割り当てることができます。 ネットワークアダプターが VMQ インターフェイスをサポートしている場合、PF に割り当てられている既定以外の VPorts は VM の受信キューにも使用できます。

NDIS\_NIC\_スイッチ\_CAP\_単一\_VPORT\_POOL フラグが設定されている場合は、使用可能な既定以外の Vport が作成され、PF と割り当てられた VFs に割り当てられます。 作成して PF に割り当てることができる VPorts の最大数は、ドライバーが**Maxnumvports**メンバーで報告するのと同じ値です。 ミニポートドライバーは、PF に割り当てられている既定の VPort として使用する VPort を1つ予約する必要があります。 その結果、PF に割り当てて VM 受信キューに使用できる既定以外の VPorts の最大数は、(**Maxnumvports**– 1) です。

> [!NOTE]
> このフラグが設定されている場合、既定以外の VPorts の作成と割り当ては、VF 割り当て用に予約されていません。 その結果、プールに使用可能な Vport がなくなった場合に、VF に VPort が割り当てられない状況が発生する可能性があります。 

NDIS\_NIC\_スイッチ\_CAP\_単一\_VPORT\_POOL フラグが設定されていない場合、既定以外の Vport の作成と割り当ては、VF 割り当て用に予約されています。 作成し、PF に割り当てて VM 受信キューに使用できる既定以外の追加の VPorts の最大数は、(**Maxnumvports**–**maxnumvfs**) です。

VMQ の詳細については、「[仮想マシンキュー (vmq)](virtual-machine-queue--vmq-.md)」を参照してください。
