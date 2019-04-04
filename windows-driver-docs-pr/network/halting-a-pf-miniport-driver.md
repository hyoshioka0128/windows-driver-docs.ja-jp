---
title: PF のミニポート ドライバーを停止します。
description: PF のミニポート ドライバーを停止します。
ms.assetid: E3F6B78E-6938-459B-883E-5DA0BB1D73C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43dba8bda1cc62e6f1cf7ed277ca022f84c94e1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536714"
---
# <a name="halting-a-pf-miniport-driver"></a>PF のミニポート ドライバーを停止します。


このトピックでは、PCI Express (PCIe) 物理機能 (PF) シングル ルート I/O 仮想化 (SR-IOV) をサポートするアダプターのミニポート ドライバーを停止に関連する手順について説明します。 次の手順は、次の図に表示されます。

![上にある、ドライバー、ndis、および、pf ミニポート ドライバーの間でどの要求と関数のフローで、完全なテキストで説明されているプロセスのイメージです。](images/sriov-pf-halt.png)

このトピックには、次の情報が含まれています。

-   [NDIS を前にドライバーを後続のアクション実行*MiniportHaltEx*が呼び出されます](#overlying-drivers)

-   [アクションの実行によって、PF ミニポート ドライバーと*MiniportHaltEx*が呼び出されます](#miniport-driver)

## <a name="actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called"></a>NDIS を前にドライバーを後続のアクション実行*MiniportHaltEx*が呼び出されます


NDIS 呼び出し、PF ミニポート ドライバーの前に[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数の場合、最初は次のこと。

-   NDIS は、基になる PF ミニポート ドライバーにバインドしたすべてのプロトコル ドライバーをバインド解除します。 NDIS は、プロトコル ドライバーの呼び出しによって[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。

-   NDIS は、基になる PF ミニポート ドライバーにバインドしたすべてのフィルター ドライバーをデタッチします。 NDIS フィルター ドライバーを呼び出すことによっては[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)関数。

ときに、上位のプロトコルまたはフィルター ドライバーのバインドを解除されているまたは PF ミニポート ドライバーからデタッチ、その次の手順。

1.  ドライバーのオブジェクト識別子 (OID) セット要求を発行する必要があります[OID\_受信\_フィルター\_オフ\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785)を設定したすべての受信フィルターをオフにします。 ドライバーは、既定の仮想ポート (VPort) または、既定以外のネットワーク アダプターで NIC スイッチの拡張のこれらのフィルターを設定します。 ドライバーの OID メソッド要求を発行してこれらのフィルターを設定する[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) PF ミニポート ドライバーにします。

2.  ドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)規定値以外の NIC のスイッチで以前に作成した拡張を削除します。 ドライバーの OID メソッド要求を発行してこれらの拡張を設定する[OID\_NIC\_スイッチ\_作成\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816) PF ミニポート ドライバーにします。

3.  ドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)どの PCIe 仮想機能 (Vf) NIC で以前割り当てられているリソースを解放するにはスイッチです。 ドライバーは、の OID メソッド要求を発行して、VF のリソースを割り当てます[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814) PF ミニポート ドライバーにします。

    詳細については、[仮想関数のリソースを解放](freeing-resources-for-a-virtual-function.md)を参照してください。

    **注**  VF 用のリソースが解放されると、NDIS を呼び出す、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388) VF ミニポート ドライバーの機能です。 詳細については、[VF のミニポート ドライバーを停止する](halting-a-vf-miniport-driver.md)を参照してください。

     

すべてのフィルター、拡張、既定以外の受信し VFs はから削除されている NIC の切り替え、NDIS が次の手順に従います。

-   NDIS の OID のセット要求を発行してすべての NIC スイッチを削除します[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)PF ミニポート ドライバーにします。 NIC のスイッチを削除する方法の詳細については、[NIC スイッチを削除する](deleting-a-nic-switch.md)を参照してください。

    **注**  以降 Windows Server 2012 では、SR-IOV インターフェイスに対してのみサポートして既定の NIC のスイッチ、ネットワーク アダプター。

     

-   NDIS が呼び出すすべての NIC スイッチが正常に削除された後、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388) PF ミニポート ドライバーの機能です。

## <a name="actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called"></a>アクションの実行によって、PF ミニポート ドライバーと*MiniportHaltEx*が呼び出されます


NDIS を呼び出すと*MiniportHaltEx*、PF ミニポート ドライバーが次の手順に従う必要があります。

1.  ドライバーが呼び出すことによってでアダプターの仮想化を無効にする必要があります、PF ミニポート ドライバーでは、NIC スイッチおよび NIC スイッチが削除されているすべての静的な作成をサポートする場合[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)で*EnableVirtualization*パラメーターが FALSE に設定し、 *NumVFs*パラメーター 0 に設定します。

    [**NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)クリア、 **NumVFs**メンバーと**VF 有効**の PCIe 構成領域で SR-IOV 拡張機能の構造内のビット、ネットワーク アダプターの PF.

    **注**  呼び出す必要がありますが、PF ミニポート ドライバーでは、動的な作成と NIC のスイッチの構成をサポートする場合[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481)ドライバーを処理すると、OID の要求を設定する[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817)します。 前にこの OID 要求が発行された*MiniportHaltEx*が呼び出されます。

     

2.  PF のミニポート ドライバーでは、ミニポート停止の操作に関連するその他のタスクを実行します。 詳細については、[ミニポート アダプターを停止する](halting-a-miniport-adapter.md)を参照してください。

 

 





