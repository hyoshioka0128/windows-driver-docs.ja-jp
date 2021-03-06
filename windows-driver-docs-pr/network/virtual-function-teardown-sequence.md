---
title: 仮想関数切断シーケンス
description: 仮想関数切断シーケンス
ms.assetid: 8C59A4F7-FC5D-4680-8CDD-751422588601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d95287c67448fc4416591cdb5d49a0fd51ae6e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354477"
---
# <a name="virtual-function-teardown-sequence"></a>仮想関数切断シーケンス


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、次のハードウェア コンポーネントをサポートできる必要があります。

-   1 つの PCI Express、(PCIe) 物理機能 (PF)。 PF は常にネットワーク アダプターに存在し、HYPER-V 親パーティションにアタッチされます。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 物理機能 (PF)](sr-iov-physical-function--pf-.md)します。

-   1 つまたは複数 PCIe 仮想機能 (VF)。 各 VF は初期化され、ゲスト オペレーティング システムのネットワーク コンポーネントを送信したり、VF 経由のパケットの受信前に、HYPER-V 子パーティションに接続されている必要があります。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

VF が切断され、そのリソースの解放、前に、仮想化スタックは、仮想 PCI (VPCI) 仮想サービス プロバイダー (VSP) を通知します。 この VSP では、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。 VF を破棄して子パーティションからデタッチされますが、通知は VPCI VSP を通知します。 VPCI VSP では、子パーティションのゲスト オペレーティング システムで実行されている VPCI 仮想サービス クライアント (VSC) に仮想マシン バス (VMBus) 経由でメッセージを送信します。 これらのメッセージは、VF が子パーティションに接続されていたときに公開されたされる VF のネットワーク アダプターを正常に削除 VPCI VSC を要求します。 これにより、VF のミニポート ドライバーと中断するドライバーからバインド解除する NetVSC です。 この時点では、子パーティションにパケット トラフィックは、VF のデータ パスから、ソフトウェア ベースの合成データ パスに移行します。 これらのデータ パスの詳細については、次を参照してください。 [SR-IOV データ パス](sr-iov-data-paths.md)します。

合成データ パスへのフェールオーバーが完了した後、VF が切断され、そのリソースを解放します。 次の図は、VF の破棄に関連する手順を示します。

![ndis してから、pf ミニポート ドライバーには仮想化スタックからの呼び出しを示す vf teardown のシーケンスの例](images/sriov-vf-teardown.png)

NDIS、仮想化スタック、および、PF ミニポート ドライバー VF 破棄シーケンス中に次の手順に従います。

1.  仮想化スタックは、メディア アクセス制御 (MAC) と既定の仮想ポートに (VPort)、PF. にアタッチされている仮想マシン (VM) ネットワーク アダプターの仮想 LAN (VLAN) をフィルター処理を移動します。 VM のネットワーク アダプターは、子パーティションのゲスト オペレーティング システムで公開されます。

    Aftet VPort の既定値にフィルターを移動、合成データ パスはネットワーク トラフィックとゲスト オペレーティング システムで実行されているネットワーク コンポーネントの間に完全に operational です。 PF のミニポート ドライバーでは、PF VPort をゲスト オペレーティング システムにパケットを示すために合成データ パスを使用する既定のパケットを受信したことを示します。 同様に、ゲスト オペレーティング システムから送信されたパケットはすべてが合成データ パス経由でルーティングし、既定の PF VPort を通じて送信します。

2.  仮想化スタックのオブジェクト識別子 (OID) セット要求を発行して、VF に関連付けられている VPort の削除[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport) PF をミニポート ドライバー。 ミニポート ドライバーは、VPort に関連付けられているハードウェアまたはソフトウェアのリソースを解放し、OID 要求を完了します。

    詳細については、次を参照してください。[仮想ポートを削除する](deleting-a-virtual-port.md)します。

3.  仮想化スタックに要求、PCIe 関数レベルではそのリソースの割り当てが解除される前に、VF の (FLR) をリセットします。 スタックの OID セット要求を発行することによって[OID\_SRIOV\_リセット\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)PF ミニポート ドライバーにします。 FLR では、VF をにより、SR-IOV ネットワーク アダプターで休止状態にし、VF の保留中の中断イベントをクリアします。

4.  仮想化スタックがの OID セット要求を発行して VF リソースの割り当て解除を要求、VF のリセット後[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf) PF をミニポート ドライバー。 これにより、ミニポート ドライバー、VF に関連付けられたハードウェア リソースを解放します。

 

 





