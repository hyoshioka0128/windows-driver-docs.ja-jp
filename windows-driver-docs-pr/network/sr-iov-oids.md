---
title: SR-IOV OID
description: このセクションでは、Single Root I/O Virtualization (SR-IOV) の Oid とその特性について説明します。
keywords:
- SR-IOV OID
- シングル ルート I/O 仮想化の Oid
- WDK SR-IOV Oid
- SR-IOV オブジェクト識別子
ms.assetid: E93751BF-17BC-4BE7-89F7-53F6C9941120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8d5b7e6859fe087c90e155432c63483bbc57e6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386209"
---
# <a name="sr-iov-oids"></a>SR-IOV OID

ミニポートと SR-IOV インターフェイスをサポートする上位のドライバーにシングル ルート I/O 仮想化 (SR-IOV) のオブジェクト識別子 (Oid) が適用されます。 このインターフェイスは、NDIS version 6.30 以降でサポートされます。 

次の表では、SR-IOV Oid の特性を定義します。 次の省略形を使用して、テーブルの Oid の特性を指定します。

- Q  
OID は、クエリ要求でのみ使用されます。
- S  
OID は、一連の要求でのみ使用されます。
- M  
OID は、メソッドの要求でのみ使用されます。 セットまたはクエリ操作のこれらの要求を発行する可能性があります。
- N  
NDIS によって直接、ミニポート ドライバーではなく、OID 要求が処理されます。 ドライバーにはこれらの Oid が発行するされません。
- P  
ネットワーク アダプターの物理機能 (PF) のミニポート ドライバーにのみ、OID 要求が発行されます。  
PF ドライバーは、これらの Oid をサポートする必要があります。 また、ドライバーでこれらの Oid を一覧する必要があります、 **SupportedOidList**のメンバー、 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造で、ドライバーに合格する、 *MiniportAttributes*への呼び出しのパラメーター [NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。
- V  
OID 要求は、ネットワークの仮想機能 (Vf) のいずれかのミニポート ドライバーにのみ発行されます。  
VF ドライバーでは、これらの Oid をサポートする必要があります。 また、ドライバーでこれらの Oid を一覧する必要があります、 **SupportedOidList**のメンバー、 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造で、ドライバーに合格する、 *MiniportAttributes*への呼び出しのパラメーター [NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

| 名前                                                                                                 | Q | S | M | N | P | V |
|---                                                                                                   |---|---|---|---|---|---|
| [OID_NIC_SWITCH_ALLOCATE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)           |   |   | x |   | x |   | 
| [OID_NIC_SWITCH_CREATE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)         |   |   | x |   | x |   | 
| [OID_NIC_SWITCH_CREATE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)          |   |   | x |   | x |   |
| [OID_NIC_SWITCH_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)  | x |   |   | x |   |   |  
| [OID_NIC_SWITCH_DELETE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)         |   | x |   |   | x |   |  
| [OID_NIC_SWITCH_DELETE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)          |   | x |   |   | x |   | 
| [OID_NIC_SWITCH_ENUM_SWITCHES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)         | x |   |   | x |   |   |   
| [OID_NIC_SWITCH_ENUM_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)              | x |   |   | x |   |   |   
| [OID_NIC_SWITCH_ENUM_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)           | x |   |   | x |   |   |  
| [OID_NIC_SWITCH_FREE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)               |   | x |   |   | x |   | 
| [OID_NIC_SWITCH_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities) | x |   |   | x |   |   |   
| [OID_NIC_SWITCH_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)            |   |   | x |   | x |   | 
| [OID_NIC_SWITCH_VF_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)         |   |   | x |   | x |   | 
| [OID_NIC_SWITCH_VPORT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)      |   |   | x |   | x |   | 
| [OID_SRIOV_BAR_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-bar-resources)              |   | x |   |   | x |   | 
| [OID_SRIOV_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)       | x |   |   | x |   |   |   
| [OID_SRIOV_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)      | x |   |   | x |   |   |   
| [OID_SRIOV_PF_LUID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-pf-luid)                    | x |   |   | x |   |   |   
| [OID_SRIOV_PROBED_BARS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)                | x |   |   |   | x |   | 
| [OID_SRIOV_READ_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-block)       |   |   | x |   | x |   | 
| [OID_SRIOV_READ_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)       |   |   | x |   | x |   | 
| [OID_SRIOV_RESET_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)                   |   | x |   |   | x |   | 
| [OID_SRIOV_SET_VF_POWER_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)         |   | x |   |   | x |   |  
| [OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block) |   |   | x |   |   | x | 
| [OID_SRIOV_VF_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-serial-number)           | x |   |   | x |   |   |   
| [OID_SRIOV_VF_VENDOR_DEVICE_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)        |   |   | x |   | x |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-block)      |   | x |   |   | x |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)      |   | x |   |   | x |   |


