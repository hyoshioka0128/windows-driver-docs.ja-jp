---
title: 仮想ポートの削除
description: 仮想ポートの削除
ms.assetid: CBE7AC59-D878-44BA-8FE6-168EC17A2D67
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 628bbc2877baaa56864fd085109c61e21cf4bf54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834927"
---
# <a name="deleting-a-virtual-port"></a>仮想ポートの削除


ネットワークアダプターの NIC スイッチ上の既定以外の仮想ポート (VPort) を削除するために[\_VPORT を削除\_vport\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)のオブジェクト識別子 (oid) セット要求を経由して、ドライバーが\_を発行します。 このドライバーは、以前に作成した VPort を削除できるのは、oid\_NIC\_スイッチの OID メソッド要求を発行して、 [\_vport\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)した場合のみです。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)へのポインターが含まれています\_VPORT\_PARAMETERS 構造体を削除\_ます。

仮想化スタックなどの前のドライバーは、以前に作成した既定以外の VPort を削除できます。 この後のドライバーでは、oid\_NIC\_スイッチの OID メソッド要求を発行して VPort を作成[\_\_VPORT を作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)します。

Oid\_NIC\_スイッチの OID セット要求を発行する前に、 [\_VPORT\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)する前に、次のドライバーを実行する必要があります。

-   このドライバーは、vport を削除する前に、ドライバーが以前に VPort に設定したすべての受信フィルターをクリアまたは移動する必要があります。 受信フィルターは、oid の OID 要求によって設定されます。 [\_受信\_フィルター\_設定\_フィルターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)し、OID の oid 要求を介して移動します\_フィルター\_[移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)\_ます。

-   このドライバーは、NDIS\_NIC\_スイッチの**VPortId**メンバーを、削除する既定以外の vport の識別子に[ **\_VPORT\_PARAMETERS 構造を削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)設定します。

    **VPortId**メンバーを**NDIS\_既定\_ポート\_番号**に設定しないようにする必要がある  に**注意**してください。 この VPort 識別子は、ネットワークアダプターの PCI Express (PCIe) 物理機能 (PF) に接続されている既定の VPort 用に予約されています。 Oid\_NIC\_スイッチの OID セット要求では、既定の VPort は常に存在し、明示的には削除されません[\_vport\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)します。

     

この後のドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、基になる PF ミニポートドライバーへの[\_VPORT 要求の削除\_、OID\_NIC\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)を発行します。 ミニポートドライバーが OID\_NIC\_を受信した場合、\_VPORT 要求を削除\_、ドライバーは次の操作を行う必要があります。

-   ドライバーは、指定された VPort に割り当てられたハードウェアとソフトウェアのリソースを解放する必要があります。

-   ドライバーは、指定された VPort を PF または PCIe 仮想関数 (VF) から切断する必要があります。

    VPort が VF に接続されている場合、仮想化スタックは、ゲストオペレーティングシステムで実行されている VF ミニポートドライバーが以前に一時停止および停止していることを確認します。 その結果、VPort からのすべての前の受信パケットが VF ミニポートドライバーに返されます。

    VPort が PF に接続されている場合、PF ミニポートドライバーは、VPort に関連付けられている共有メモリに対して追加の DMA を停止する必要があります。 PF ミニポートドライバーは、VPort からのすべての前の受信パケットがミニポートに返されるようにする必要があります。 PF ミニポートドライバーは、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体に含まれる vport の識別子を指定する追加の受信通知を NDIS に提供しないようにする必要があります。 VPort からのすべての受信パケットが PF ミニポートドライバーに返されたら、 [**NdisFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreesharedmemory)を呼び出して、vport に関連付けられている共有メモリを解放する必要があります。

VPorts の削除には、次の点が適用されます。

-   プロトコルドライバーは、 [**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)を呼び出す前に、作成したすべての既定以外の vports を削除する必要があります。

-   このフィルタードライバーは、 [*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数内に作成された既定以外のすべての vports を削除する必要があります。

-   NDIS が OID\_NIC のセット要求を発行する前に[\_スイッチを削除\_\_スイッチを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)してネットワークアダプターの nic スイッチを削除すると、既定以外のすべての vports がそのスイッチから削除されることが保証されます。

-   Oid\_の oid 要求を使用して明示的に削除できるのは、既定以外の VPorts だけです[\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 既定の VPort は、PF ミニポートドライバーによって既定の NIC スイッチが削除されると、暗黙的に削除されます。 詳細については、「 [NIC スイッチの削除](deleting-a-nic-switch.md)」を参照してください。

 

 





