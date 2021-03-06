---
title: 仮想関数初期化シーケンス
description: 仮想関数初期化シーケンス
ms.assetid: 352E12EC-FAF0-4566-8632-B6DA97ACCAD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45a3186272e63033213e7cc267ffd99e4054dd9f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354496"
---
# <a name="virtual-function-initialization-sequence"></a>仮想関数初期化シーケンス


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、次のハードウェア コンポーネントをサポートできる必要があります。

-   1 つの PCI Express、(PCIe) 物理機能 (PF)。 PF は常にネットワーク アダプターに存在し、HYPER-V 親パーティションにアタッチされます。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 物理機能 (PF)](sr-iov-physical-function--pf-.md)します。

-   1 つまたは複数 PCIe 仮想機能 (VF)。 各 VF は初期化され、ゲスト オペレーティング システムのネットワーク コンポーネントを送信したり、VF 経由のパケットの受信前に、HYPER-V 子パーティションに接続されている必要があります。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

HYPER-V 親パーティションの管理オペレーティング システムで実行され、PF ミニポート ドライバーを初期化し、SR-IOV ネットワーク アダプター上の VF にリソースを割り当てます。 NDIS 呼び出し、PF ミニポート ドライバーの後に[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、NDIS、および仮想化スタックできますオブジェクト識別子 (OID) に要求を発行、次を行う PF ミニポート ドライバー。

-   ネットワーク アダプターで NIC スイッチを作成します。 VFs、PF、および物理ネットワーク ポート間のブリッジ ネットワーク トラフィックを NIC に切り替えます。

    詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

    **注**以降 Windows Server 2012 では、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。



-   PF のミニポート ドライバーを初期化し、リソース、ネットワーク アダプターの VF を割り当てることを要求します。

    詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

-   NIC のスイッチの仮想ポート (VPort) を作成し、VF にアタッチします。

    詳細については、次を参照してください。[仮想ポート (拡張)](virtual-ports--vports-.md)します。

次の図は、VF の初期化に関連する手順を示します。

![ndis してから、pf ミニポート ドライバーには仮想化スタックからの呼び出しを示す例 vf の初期化シーケンス](images/sriov-vf-initialization.png)

NDIS、仮想化スタック、および、PF ミニポート ドライバーは、VF の初期化シーケンス中に次の手順に従ってください。

1.  NDIS スイッチの既定の構成をレジストリから読み取るし、OID メソッド要求の発行[OID\_NIC\_切り替える\_作成\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)スイッチのネットワークをプロビジョニングするにはアダプター。 この OID 要求で渡されるパラメーターには、Vf と拡張などの重要なハードウェア リソースを構成する方法に関する情報が含まれます。 PF. にアタッチされている既定以外の拡張および既定 VPort の間でリソースを配布する方法に関する情報も含まれています。

    OID が PF ミニポート ドライバーが正常に完了した後、NIC のスイッチは拡張を作成し、VFs を割り当てるに使用する準備が。

    NIC のスイッチを作成する方法の詳細については、次を参照してください。 [NIC スイッチの作成](creating-a-nic-switch.md)です。

2.  VF は、仮想マシン (VM) ネットワーク アダプターのオフロード メカニズムとして扱われます。 このアダプターは、HYPER-V 子パーティションで実行されているゲスト オペレーティング システムで公開されます。 既定では、ゲスト オペレーティング システムのネットワーク コンポーネントは送信し、ソフトウェア ベースの合成データ パス上でパケットを受信します。 ただし、子パーティションが有効になっている場合は、VF のオフロード用の仮想化スタックがリソースの割り当てや、VF の初期化を PF ミニポート ドライバーに OID 要求を発行します。 子パーティションを NIC スイッチ上の VPort VF が接続されると、ネットワーク コンポーネントは送信し、VF データ パス上でパケットを受信します。 これらのデータ パスの詳細については、次を参照してください。 [SR-IOV データ パス](sr-iov-data-paths.md)します。

    VF オフロード、仮想化スタックの問題が、OID メソッド要求の HYPER-V 子パーティションを有効になっている場合[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf) PF ミニポートにドライバー。 この OID 要求で渡されるパラメーターは、NIC の識別子を含める VF が割り当てられているをオンにします。 その他のパラメーターには、VF のアタッチ先の子パーティションの識別子が含まれます。

    PF のミニポート ドライバーは VF のために必要なハードウェアおよびソフトウェア リソースを割り当てます。 PF のミニポート ドライバーも決定 PCIe リクエスター識別子 (RID)、VF の呼び出して[ **NdisMGetVirtualFunctionLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetvirtualfunctionlocation)します。 DMA RID が使用され、VF によって、DMA が要求したときに再マップの割り込みおよび割り込みが生成されます。

    正常に完了すると、VF の識別子と一緒に RID は、PF ミニポート ドライバーによって返される、 [OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)要求。

    VF のリソース割り当ての詳細については、次を参照してください。[仮想関数のリソースを割り当てる](allocating-resources-for-a-virtual-function.md)します。

3.  仮想化スタックの OID メソッド要求を発行して、NIC のスイッチで、VPort を作成します[OID\_NIC\_切り替える\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport) PF ミニポート ドライバーにします。 この OID 要求で渡されるパラメーターには、NIC のスイッチの識別子が含まれます。 これは作成するには、VPort で。 その他のパラメーターには、VF、VPort のアタッチ先の識別子が含まれます。

    **注**VPort NIC スイッチでは、常に存在し、PF. にアタッチされて、既定値 既定 VPort 単一以外のみを作成し、VF にアタッチできます。

    NDIS は、PF ミニポート ドライバーに OID 要求を転送する前に、ネットワーク アダプタ上で一意である有効な VPort 識別子を割り当てます。

    PF のミニポート ドライバーでは、OID 要求を処理する場合は、VPort に必要なハードウェア リソースが割り当てられ、VPort の識別子を保持します。 この識別子は、以降の OID 要求と、SR-IOV 関数の呼び出しで使用されます。

    VPort を作成する方法の詳細については、次を参照してください。[仮想ポートを作成する](creating-a-virtual-port.md)します。

4.  VF と VPort が割り当てられる前に時間の長い、HYPER-V 子パーティションを開始することがあります。 この期間中、ゲスト オペレーティング システムのネットワーク コンポーネントは送信し、合成データ パス上でパケットを受信します。 これは、既定、PF. に関連付けられている VPort 経由でトラフィック パケットにはが含まれます 子パーティションへのトラフィックをブリッジするには、は、仮想化スタックは、メディア アクセス コントロール (MAC) と子パーティションの VM ネットワーク アダプターの仮想 LAN (VLAN) フィルター VPort の既定値を構成します。

    リソースの後、VF と VPort が割り当てられているの仮想化スタック要求を発行 OID メソッドの[OID\_受信\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter) PF ミニポート ドライバーに. この OID 要求では、VM のネットワーク アダプターの MAC、および VLAN のフィルターを既定 VPort から VF に関連付けられている VPort に移動します。 これにより、VF VPort に VF のデータ パス経由で転送されるこれらのフィルターに一致するパケットです。

    **注**既存のフィルターが表示される可能性がありますから移動既定 VPort VF VPort を使用して[OID\_受信\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)します。 使用して、VF VPort が新しいフィルターを設定できますまた、 [OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。

VF と、VPort が正常に作成し、VPort MAC フィルターが設定されている、仮想化スタックは、仮想 PCI (VPCI) 仮想サービス プロバイダー (VSP) を通知します。 この VSP では、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。 VPCI VSP を示す通知を正常に割り当てられたおよび子パーティションにアタッチされた VF します。 VPCI VSP では、子パーティションのゲスト オペレーティング システムで実行されている VPCI 仮想サービス クライアント (VSC) に仮想マシン バス (VMBus) 経由でメッセージを送信します。 VPCI VSC は、PCI デバイス VF のネットワーク アダプターを公開するバス ドライバーです。

VF のネットワーク アダプターは、公開した後、ゲスト オペレーティング システムで実行されている、PnP サブシステムはアダプターを検出し、VF のミニポート ドライバーを読み込みます。 このドライバーは、NDIS を登録します。 VF のミニポート ドライバーが初期化されているし、VF のネットワーク アダプターで適切なパケット フィルターを構成、VF のデータ パスが完全に動作します。 その結果、ゲスト オペレーティング システムにパケット トラフィックは、データ パスに、合成データ パスから切り替えました。