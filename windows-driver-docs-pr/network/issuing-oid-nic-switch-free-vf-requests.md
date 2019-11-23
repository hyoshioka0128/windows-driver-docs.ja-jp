---
title: OID_NIC_SWITCH_FREE_VF 要求の発行
description: OID_NIC_SWITCH_FREE_VF 要求の発行
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06eb856d509f1d09b3b63cf1982e86840e476143
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844151"
---
# <a name="issuing-oid_nic_switch_free_vf-requests"></a>OID\_NIC の発行\_スイッチ\_の\_VF 要求の解放


それより後のドライバーは、Oid (オブジェクト識別子) セット要求を発行して[\_NIC\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)を使用して\_VF を解放し、PCI Express (PCIe) 仮想機能 (vf) のリソースを解放します。 これらのリソースは、以前は oid の OID メソッド要求を通じて割り当てられていました。 [\_NIC\_スイッチ\_割り当て\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)です。

この後のドライバーは、 [OID\_NIC\_スイッチに\_\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)セット要求を PCIe 物理機能 (PF) のミニポートドライバーに発行します。 この OID 要求を発行する前に、次のことを行う必要があります。

1.  このドライバーは、ネットワークアダプターの NIC スイッチの仮想ポート (VPort) に VF がアタッチされていないことを確認する必要があります。 この後のドライバーは、 [oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)の oid セット要求を発行する必要があります。\_VPORT を削除して、VF に接続されているすべての vport を削除\_ます。 詳細については、「[仮想ポートの削除](deleting-a-virtual-port.md)」を参照してください。

2.  このドライバーは、 [**NDIS\_NIC\_スイッチを初期化し\_\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)構造体を解放します。 ドライバーは、 **VFId**メンバーを、oid メソッド要求 oid\_\_で返された vf 識別子に設定する必要があります。これは[\_vf\_割り当て](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。

この後のドライバーは、次の手順に従って、 [oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)の oid セット要求を\_VF\_解放します。

1.  前のドライバーは、OID メソッド要求の[**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を初期化します。 ドライバーは、初期化された NDIS\_NIC\_スイッチへのポインターに**Informationbuffer**メンバーを設定[ **\_\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)構造体を解放します。

2.  前のドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、基になる PF ミニポートドライバーに OID 要求を発行します。

あるドライバーが VF のリソース割り当てを要求した後、そのドライバーは、同じ VF のリソースの解放を要求できる唯一のコンポーネントです。 この後のドライバーは、oid\_NIC の OID セット要求を発行する必要があります。これは、 [\_空き\_vf の\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)によって、vf リソースが解放されます。 前のドライバーを停止する前に、ドライバーの[OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)によって割り当てられた各 vf のリソースを解放して\_VF 要求の割り当て\_する必要があります。

**注**   OID [\_NIC\_\_\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)の oid メソッド要求を発行すると、vf のリソースを割り当てるために、そのドライバーは、同じ vf のリソースの解放を要求できる唯一のコンポーネントとなります。 この後のドライバーは、oid\_NIC の OID セット要求を発行する必要があります。これは、 [\_空き\_vf の\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)によって、vf リソースが解放されます。 前のドライバーを停止する前に、ドライバーの OID\_NIC\_スイッチによって割り当てられた各 VF のリソースを解放して\_VF 要求の割り当て\_する必要があります。

 

 

 





