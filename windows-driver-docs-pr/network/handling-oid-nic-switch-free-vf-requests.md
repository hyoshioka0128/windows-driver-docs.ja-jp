---
title: OID_NIC_SWITCH_FREE_VF 要求の処理
description: OID_NIC_SWITCH_FREE_VF 要求の処理
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da425eed0725953e4078ce0775d472ef9e0fc296
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842580"
---
# <a name="handling-oid_nic_switch_free_vf-requests"></a>OID\_NIC を処理する\_スイッチ\_の\_VF 要求を解放する


ネットワークアダプター上の PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーがオブジェクト識別子 (OID) の set 要求を処理するときに、 [\_NIC\_スイッチの\_VF\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)は、次の処理を実行します。

-   OID 要求の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)へのポインターが含まれています。これには、\_の VF\_PARAMETERS 構造が無料で\_ます。 PF ミニポートドライバーは、 **VFId**メンバーによって指定された PCIe 仮想関数 (VF) の識別子が有効であることを確認する必要があります。 これが true でない場合、ドライバーは、NDIS\_STATUS\_無効な\_パラメーターを返すことによって、OID セット要求を失敗させる必要があります。

-   PF ミニポートドライバーは、VF のリソースが以前に oid [\_\_\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)の oid 要求を通じて割り当てられていることを検証する必要があります。 これが true でない場合、ドライバーは、NDIS\_STATUS\_無効な\_パラメーターを返すことによって、OID セット要求を失敗させる必要があります。

-   PF ミニポートドライバーは、現在 VF に接続されている仮想ポート (VPorts) がないことを確認する必要があります。 これが true でない場合、ドライバーは、NDIS\_STATUS\_無効な\_パラメーターを返すことによって、set 要求を失敗させる必要があります。

-   PF ミニポートドライバーは、指定された VF に割り当てられたすべてのソフトウェアリソースを解放する必要があります。

-   PF ミニポートドライバーは、ネットワークアダプターの NIC スイッチから VF を切断する必要があります。

PF ミニポートドライバーが、割り当てられたソフトウェアリソースを正常に解放し、NIC スイッチから VF を切断できる場合、ドライバーは NDIS\_STATUS\_SUCCESS の OID 要求を完了します。

**  ndis**では、ndis が oid を発行する前に、ミニポートに割り当てられているすべての VFs が解放されることを保証します。これにより、 [\_NIC\_スイッチ\_削除\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch) 、PF ミニポートドライバーに切り替えます。 この OID を処理すると、ドライバーはネットワークアダプターの NIC スイッチを削除します。

 

 

 





