---
title: 仮想関数初期化シーケンス
description: 仮想関数初期化シーケンス
ms.assetid: 352E12EC-FAF0-4566-8632-B6DA97ACCAD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabd7e9edd1b42d6b01c7c10a62342385683388e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842954"
---
# <a name="virtual-function-initialization-sequence"></a>仮想関数初期化シーケンス


シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターは、次のハードウェアコンポーネントをサポートしている必要があります。

-   1つの PCI Express (PCIe) 物理機能 (PF)。 PF は常にネットワークアダプターに存在し、Hyper-v の親パーティションに接続されています。

    このハードウェアコンポーネントの詳細については、「sr-iov[物理機能 (PF)](sr-iov-physical-function--pf-.md)」を参照してください。

-   1つまたは複数の PCIe 仮想関数 (VF)。 各 VF を初期化し、Hyper-v の子パーティションに接続してから、ゲストオペレーティングシステムのネットワークコンポーネントが VF を介してパケットを送受信できるようにする必要があります。

    このハードウェアコンポーネントの詳細については、「 [Sr-iov 仮想機能 (VFs)](sr-iov-virtual-functions--vfs-.md)」を参照してください。

Hyper-v 親パーティションの管理オペレーティングシステムで実行される PF ミニポートドライバーは、SR-IOV ネットワークアダプターの VF のリソースを初期化して割り当てます。 NDIS が PF ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出した後、ndis および仮想化スタックは、次の操作を実行するために、オブジェクト識別子 (OID) 要求を pf ミニポートドライバーに発行できます。

-   ネットワークアダプターに NIC スイッチを作成します。 NIC スイッチは、VFs、PF、および物理ネットワークポート間のネットワークトラフィックをブリッジします。

    詳細については、「 [NIC スイッチ](nic-switches.md)」を参照してください。

    **メモ** Windows Server 2012 以降では、SR-IOV インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。



-   ネットワークアダプターの VF 用にリソースを初期化して割り当てるように、PF ミニポートドライバーに要求します。

    詳細については、「sr-iov[仮想関数 (VFs)](sr-iov-virtual-functions--vfs-.md)」を参照してください。

-   NIC スイッチに仮想ポート (VPort) を作成し、それを VF に接続します。

    詳細については、「[仮想ポート (vports)](virtual-ports--vports-.md)」を参照してください。

次の図は、VF の初期化に関連する手順を示しています。

![仮想化スタックから ndis への呼び出しと、pf ミニポートドライバーへの呼び出しを示す、vf 初期化シーケンスの例](images/sriov-vf-initialization.png)

NDIS、仮想化スタック、および PF ミニポートドライバーは、VF 初期化シーケンス中に次の手順を実行します。

1.  NDIS はレジストリから既定のスイッチ構成を読み取り、oid [\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)の oid メソッド要求を発行\_\_スイッチを作成して、ネットワークアダプターでスイッチをプロビジョニングします。 この OID 要求で渡されるパラメーターには、VFs や VPorts などの重要なハードウェアリソースを構成する方法に関する情報が含まれます。 また、既定以外の VPorts と、PF に接続されている既定の Vports の間でリソースを分散する方法についても説明します。

    PF ミニポートドライバーによって OID が正常に完了したら、NIC スイッチを使用して VPorts を作成し、VFs を割り当てることができます。

    NIC スイッチを作成する方法の詳細については、「 [Nic スイッチの作成](creating-a-nic-switch.md)」を参照してください。

2.  VF は、仮想マシン (VM) ネットワークアダプターのオフロードメカニズムとして扱われます。 このアダプターは、Hyper-v 子パーティションで実行されているゲストオペレーティングシステムで公開されています。 既定では、ゲストオペレーティングシステムのネットワークコンポーネントは、ソフトウェアベースの合成データパスを介してパケットを送受信します。 ただし、子パーティションで VF オフロードが有効になっている場合、仮想化スタックは、VF のリソース割り当てと初期化のために、PF ミニポートドライバーに対して OID 要求を発行します。 VF が子パーティションに接続され、NIC スイッチに VPort が接続されると、ネットワークコンポーネントは VF データパスを介してパケットを送受信します。 これらのデータパスの詳細については、「sr-iov[データパス](sr-iov-data-paths.md)」を参照してください。

    Hyper-v の子パーティションで VF オフロードが有効になっている場合、仮想化スタックは oid\_の oid メソッド要求を発行します。これは、\_VF を PF ミニポートドライバーに[割り当てる\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)です。 この OID 要求で渡されるパラメーターには、VF が割り当てられている NIC スイッチの識別子が含まれます。 その他のパラメーターには、VF がアタッチされる子パーティションの識別子が含まれます。

    PF ミニポートドライバーは、必要なハードウェアとソフトウェアのリソースを VF に割り当てます。 また、PF ミニポートドライバーは、 [**NdisMGetVirtualFunctionLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionlocation)を呼び出すことによって、VF の PCIe 要求識別子 (RID) を決定します。 VF は、dma 要求と割り込みが VF によって生成されるときに、DMA と割り込み再マップに使用されます。

    [OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)が正常に完了したときに、PF ミニポートドライバーによって RID 識別子と共に RID が返され、\_VF 要求の割り当て\_ます。

    VF のリソース割り当ての詳細については、「[仮想関数のリソースの割り当て](allocating-resources-for-a-virtual-function.md)」を参照してください。

3.  仮想化スタックは、oid\_NIC\_スイッチの OID メソッド要求を発行することによって、NIC スイッチに VPort を作成し、PF ミニポートドライバーに[\_VPORT を作成\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)ます。 この OID 要求で渡されるパラメーターには、VPort を作成する NIC スイッチの識別子が含まれます。 その他のパラメーターには、VPort が接続される VF の識別子が含まれます。

    **メモ** NIC スイッチの既定の VPort は常に存在し、PF に接続されています。 1つの既定以外の VPort だけを作成して、VF に接続できます。

    NDIS が OID 要求を PF ミニポートドライバーに転送する前に、ネットワークアダプター上で一意の有効な VPort 識別子が割り当てられます。

    PF ミニポートドライバーは OID 要求を処理するときに、VPort に必要なハードウェアリソースを割り当て、VPort の識別子を保持します。 この識別子は、後の OID 要求および SR-IOV の関数呼び出しで使用されます。

    VPort の作成方法の詳細については、「[仮想ポートの](creating-a-virtual-port.md)作成」を参照してください。

4.  Hyper-v 子パーティションは、VF と VPort が割り当てられる前に長時間開始されることがあります。 この間、ゲストオペレーティングシステムのネットワークコンポーネントは、合成データパスを介してパケットを送受信します。 これには、PF に接続されている既定の VPort に対するパケットトラフィックが含まれます。 子パーティションにトラフィックをブリッジするために、仮想化スタックは、子パーティションの VM ネットワークアダプターのメディアアクセス制御 (MAC) フィルターと仮想 LAN (VLAN) フィルターを使用して、既定の VPort を構成します。

    VF と VPort のリソースが割り当てられると、仮想化スタックによって oid の OID メソッド要求が発行され\_\_フィルター\_、PF ミニポートドライバーに[\_フィルターが移動さ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)れます。 この OID 要求は、VM ネットワークアダプターの MAC および VLAN フィルターを、既定の VPort から VF に接続されている VPort に移動します。 これにより、これらのフィルターに一致するパケットが VF データパス経由で VF VPort に転送されます。

    **メモ** 既存の受信フィルターは、OID を使用して既定の VPort から VF VPort に移動できます。その場合は、 [\_フィルター\_移動し、\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)ます。 また、 [\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)を使用\_して、VF vport に新しいフィルターを設定することもできます。

VF と VPort が正常に作成され、VPort に MAC フィルターが設定されると、仮想化スタックは仮想 PCI (VPCI) 仮想サービスプロバイダー (VSP) に通知します。 この VSP は、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。 この通知は、正常に割り当てられ、子パーティションにアタッチされた VF を VPCI VSP に通知します。 VPCI VSP は、仮想マシンバス (VMBus) を介して、子パーティションのゲストオペレーティングシステムで実行されている VPCI 仮想サービスクライアント (VSC) にメッセージを送信します。 VPCI VSC は、VF ネットワークアダプターの PCI デバイスを公開するバスドライバーです。

VF ネットワークアダプターが公開されると、ゲストオペレーティングシステムで実行される PnP サブシステムがアダプターを検出し、VF ミニポートドライバーを読み込みます。 このドライバーは、NDIS に登録します。 Vf ミニポートドライバーが初期化され、適切なパケットフィルターが VF ネットワークアダプターで構成されると、VF データパスは完全に動作します。 その結果、ゲストオペレーティングシステムのパケットトラフィックは、合成データパスからこのデータパスに切り替えられます。