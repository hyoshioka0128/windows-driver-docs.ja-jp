---
title: NIC スイッチの削除
description: NIC スイッチの削除
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a5b494625a668b06e514a4401057ad3bcf33a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838165"
---
# <a name="deleting-a-nic-switch"></a>NIC スイッチの削除


シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターでは、NIC スイッチを削除できなければなりません。 アダプターの NIC スイッチを削除できるのは、SR-IOV アダプターの PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーだけです。

**注**  Windows Server 2012 の NDIS 6.30 以降では、sr-iov インターフェイスはネットワークアダプター上で1つの NIC スイッチのみをサポートしています。 このスイッチは*既定の NIC スイッチ*と呼ばれ、NDIS\_既定\_スイッチ\_ID 識別子によって参照されます。

 

PF ミニポートドライバーを停止する前に、NDIS は\_\_Oid のオブジェクト識別子 (OID) セット要求を発行することによって NIC スイッチを削除[\_スイッチ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)へのポインターが含まれています\_\_スイッチを指定するパラメーター構造を削除\_スイッチ\_削除されるスイッチの識別子。

NDIS では、 [oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)の oid セット要求を発行する前に、次のポリシーが適用されます。\_削除\_、PF ミニポートドライバーに切り替えます。

-   NDIS では、NIC スイッチの既定の仮想ポート (VPorts) からすべての受信フィルターがクリアされていることを保証します。 受信フィルターは、oid の OID セット要求によってクリアされます。 [\_受信\_フィルター\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)です。

-   NDIS は、スイッチ上で作成されたすべての既定以外の仮想ポート (VPorts) が既に削除されていることを保証します。 VPorts は oid [\_\_\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)の oid セット要求によって削除されます。

-   NDIS は、NIC スイッチに接続されている PCIe 仮想機能 (VFs) のすべてのリソースが既に解放されていることを保証します。 VFs は oid の oid セット要求を使用して解放されます[\_NIC\_スイッチ\_空き\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)です。

Oid\_\_スイッチの oid メソッド要求を受信すると[\_スイッチ\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)されますが、PF ミニポートドライバーは次の操作を行う必要があります。

1.  PF ミニポートドライバーが NIC スイッチの静的な作成と構成をサポートしている場合は、指定された NIC スイッチに関連付けられているソフトウェアリソースを解放する必要があります。 ただし、ドライバーは、[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が呼び出されたときにのみ、NIC スイッチのハードウェアリソースを解放できます。

    静的 NIC スイッチの作成の詳細については、「 [Nic スイッチの静的作成](static-creation-of-a-nic-switch.md)」を参照してください。

2.  PF ミニポートドライバーが NIC スイッチの動的作成と構成をサポートしている場合は、指定された NIC スイッチに関連付けられているハードウェアおよびソフトウェアリソースを解放する必要があります。

    動的な NIC スイッチの作成の詳細については、「 [Nic スイッチの動的作成](dynamic-creation-of-a-nic-switch.md)」を参照してください。

3.  PF ミニポートドライバーが NIC スイッチの動的作成をサポートしていて、すべての NIC スイッチがネットワークアダプター上で削除されている場合、ドライバーは[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出すことによって、アダプターの仮想化を無効にする必要があります。 仮想化を無効にするには、ネットワークアダプターで*Enablevirtualization*パラメーターを FALSE に設定し、 *numvfs*パラメーターを0に設定する必要があります。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)は、ネットワークアダプターの PF の PCIe 構成領域にある Sr-iov の拡張機能構造で、 **numvfs**メンバーと**VF 有効化**ビットをクリアします。

    **注**  PF ミニポートドライバーが NIC スイッチの静的な作成と構成をサポートしている場合は、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)が呼び出されたときにのみ[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出す必要があります。

     

 

 





