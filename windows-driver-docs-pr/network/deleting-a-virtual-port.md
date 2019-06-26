---
title: 仮想ポートの削除
description: 仮想ポートの削除
ms.assetid: CBE7AC59-D878-44BA-8FE6-168EC17A2D67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0c565b9898a33be0e8c3c58941d59a2dbbc58e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384561"
---
# <a name="deleting-a-virtual-port"></a>仮想ポートの削除


上位のドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)ネットワーク アダプターの既定以外の仮想ポート (VPort) を削除するにはNIC のスイッチです。 上にあるドライバーが削除できるがの OID メソッド要求を発行して以前作成した VPort だけ[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)構造体。

など、仮想化スタックの上にあるドライバーは、既定以外が以前に作成した VPort を削除できます。 上にあるドライバーの OID メソッド要求を発行して、VPort を作成します[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

OID のセット要求を発行する前に[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)、上にあるドライバーは、次を実行する必要があります。

-   上にあるドライバーをオフにまたは、すべての受信、ドライバーは以前、VPort 上、VPort の削除する前に設定するフィルターを移動する必要があります。 受信の OID 要求のフィルターが設定[OID\_受信\_フィルター\_設定\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)が移動の OID 要求を通じて[OID\_受信\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)します。

-   上にあるドライバー セット、 **VPortId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_削除\_VPORT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)構造体を削除する VPort 既定以外の識別子。

    **注**  上にあるドライバーを設定する必要がありますいない、 **VPortId**メンバー **NDIS\_既定\_ポート\_数**。 この VPort 識別子は、既定値を PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターに関連付けられている VPort の予約されています。 VPort は常に存在し、OID の要求を設定する場合と明示的に削除されませんが、既定[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。

     

上にあるドライバー呼び出し[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)問題を[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)基になる PF ミニポート ドライバーに要求します。 ミニポート ドライバーが、OID を受信すると\_NIC\_スイッチ\_削除\_VPORT 要求と、ドライバーは、次を実行する必要があります。

-   ドライバーは、指定した VPort の割り当てられたハードウェアとソフトウェアのリソースを解放する必要があります。

-   ドライバーは、PF または PCIe 仮想機能 (VF) から指定した VPort をデタッチする必要があります。

    VPort が、VF に接続されている場合、仮想化スタックにより、ゲスト オペレーティング システムで実行されている VF ミニポート ドライバーがされて以前一時停止され (停止)。 その結果、すべて previouslyindicated がパケットを受信、VPort から VF ミニポート ドライバーに返される必要があります。

    VPort が PF に接続されている場合、PF ミニポート ドライバーは、VPort に関連付けられている共有メモリを追加、DMA を停止する必要があります。 PF のミニポート ドライバーがすべて previouslyindicated が、VPort からパケットを受信することを確認してください、ミニポートに返されます。 PF ミニポート ドライバーを追加する必要があります行わない受信パケットの VPort の識別子を指定する NDIS に表示[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 パケットの受信、VPort からすべての後に返されます、PF ミニポート ドライバーでは、呼び出すことによって、VPort に関連付けられている共有メモリを解放する必要があります[ **NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreesharedmemory)します。

次の点は、拡張の削除に適用されます。

-   上位のプロトコル ドライバーに拡張する前に作成した既定値以外のすべてを削除する必要がありますを呼び出す[ **NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)します。

-   上にあるフィルター ドライバーは、拡張内で作成した既定値以外のすべてを削除する必要があります、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数。

-   NDIS のセット要求を発行する前に[OID\_NIC\_切り替える\_削除\_切り替える](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)ネットワーク アダプターで NIC スイッチを削除するのにはすべて既定以外の拡張が削除されたことを保証そのスイッチ。

-   既定の OID 要求を通じて、拡張を明示的に削除できる以外のみ[OID\_NIC\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)します。 PF のミニポート ドライバーが既定の NIC スイッチを削除するときに既定 VPort は暗黙的に削除されます。 詳細については、次を参照してください。 [NIC スイッチを削除する](deleting-a-nic-switch.md)します。

 

 





