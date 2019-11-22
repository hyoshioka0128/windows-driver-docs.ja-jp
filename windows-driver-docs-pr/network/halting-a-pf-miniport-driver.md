---
title: PF ミニポート ドライバーの停止
description: PF ミニポート ドライバーの停止
ms.assetid: E3F6B78E-6938-459B-883E-5DA0BB1D73C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a85bd4d2b1de1ff1091a23f8f6259540ad7c953
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840482"
---
# <a name="halting-a-pf-miniport-driver"></a>PF ミニポート ドライバーの停止


このトピックでは、シングルルート i/o 仮想化 (SR-IOV) をサポートするアダプターでの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーの停止に関連する手順について説明します。 これらの手順を次の図に示します。

![フルテキストで説明されているプロセスのイメージ。この場合、要求と関数は、その後のドライバー、ndis、および pf ミニポートドライバーの間でフローされます。](images/sriov-pf-halt.png)

このトピックの内容は次のとおりです。

-   [*Miniporthaltex*が呼び出される前に NDIS およびそれ以降のドライバーによって実行されるアクション](#actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called)

-   [*Miniporthaltex*が呼び出されたときに、PF ミニポートドライバーによって実行されるアクション](#actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called)

## <a name="actions-performed-by-ndis-and-overlying-drivers-before-miniporthaltex-is-called"></a>*Miniporthaltex*が呼び出される前に NDIS およびそれ以降のドライバーによって実行されるアクション


NDIS が PF ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出す前に、まず次のことを行います。

-   NDIS は、以前に基になる PF ミニポートドライバーにバインドされているすべてのプロトコルドライバーをバインド解除します。 NDIS は、プロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出すことによってこれを行います。

-   NDIS は、以前に基になる PF ミニポートドライバーにバインドされているすべてのフィルタードライバーをデタッチします。 NDIS は、フィルタードライバーの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出すことによってこれを行います。

プロトコルまたはフィルタードライバーのバインドを解除するか、PF ミニポートドライバーから切断する場合は、次の手順に従う必要があります。

1.  ドライバーは、Oid のオブジェクト識別子 (OID) セット要求を発行する必要があります。 [\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)を適用して、以前に設定した受信フィルターをクリアします。 ドライバーは、ネットワークアダプターの NIC スイッチの既定の仮想ポート (VPort) または既定以外の仮想ポートにこれらのフィルターを設定します。 このドライバーは、\_Oid の OID メソッド要求を発行することによってこれらのフィルターを設定し、 [\_フィルター\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)して、PF ミニポートドライバーに\_フィルターを設定します。

2.  ドライバーは oid [\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)の oid セット要求を発行する必要があります。\_vport を削除して、nic スイッチで以前に作成した既定以外の vport を削除\_ます。 このドライバーは、 [oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)の oid メソッド要求を発行することによってこれらの vports を設定し、PF ミニポートドライバーに\_vports を作成\_ます。

3.  ドライバーは oid [\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)の oid セット要求を発行する必要があります。これにより、nic スイッチで以前に割り当てられたすべての PCIe 仮想機能 (VFs) のリソースを解放\_\_ます。 このドライバーは、Oid の OID メソッド要求を発行することによって、VF のリソースを割り当てます。 [\_NIC\_スイッチ\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf) 、PF ミニポートドライバーに\_VF を割り当てます。

    詳細については、「[仮想関数のリソースの解放](freeing-resources-for-a-virtual-function.md)」を参照してください。

    **  vf**のリソースが解放されると、NDIS は vf ミニポートドライバーの[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 詳細については、「 [VF ミニポートドライバーの停止](halting-a-vf-miniport-driver.md)」を参照してください。

     

すべての受信フィルター、既定以外の VPorts、および VFs が NIC スイッチから削除された後、NDIS は次の手順を実行します。

-   NDIS では、 [oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)の oid セット要求を発行することによってすべての nic スイッチが削除されます。この場合\_削除\_、PF ミニポートドライバーに切り替えます。 NIC スイッチの削除方法の詳細については、「 [Nic スイッチの削除](deleting-a-nic-switch.md)」を参照してください。

    **注**  Windows Server 2012 以降では、sr-iov インターフェイスはネットワークアダプターの既定の NIC スイッチのみをサポートしています。

     

-   すべての NIC スイッチが正常に削除されると、NDIS は PF ミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。

## <a name="actions-performed-by-the-pf-miniport-driver-when-miniporthaltex-is-called"></a>*Miniporthaltex*が呼び出されたときに、PF ミニポートドライバーによって実行されるアクション


NDIS が*Miniporthaltex*を呼び出すとき、PF ミニポートドライバーは次の手順に従う必要があります。

1.  PF ミニポートドライバーが NIC スイッチの静的な作成をサポートしていて、すべての NIC スイッチが削除されている場合、ドライバーは、 *Enablevirtualization* PARAMETER を FALSE に設定し、 *numvfs*パラメーターを0に設定[**して、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)アダプターの仮想化を無効にする必要があります。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)は、ネットワークアダプターの PF の PCIe 構成領域にある Sr-iov の拡張機能構造で、 **numvfs**メンバーと**VF 有効化**ビットをクリアします。

    **注**  PF ミニポートドライバーが nic スイッチの動的な作成と構成をサポートしている場合は、ドライバーが OID の oid 設定要求を処理するときに、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出す必要があり[\_nic\_スイッチ\_\_スイッチを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)します。 この OID 要求は、 *Miniporthaltex*が呼び出される前に発行されます。

     

2.  PF ミニポートドライバーは、ミニポート停止操作に関連付けられている他のタスクを実行します。 詳細については、「[ミニポートアダプターの停止](halting-a-miniport-adapter.md)」を参照してください。

 

 





