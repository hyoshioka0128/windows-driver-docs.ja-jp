---
title: SR-IOV Oid
description: このセクションでは、シングルルート i/o 仮想化 (SR-IOV) Oid とその特性について説明します。
keywords:
- SR-IOV Oid
- シングルルート i/o 仮想化 Oid
- WDK SR-IOV Oid
- Sr-iov オブジェクト識別子
ms.assetid: E93751BF-17BC-4BE7-89F7-53F6C9941120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e39b18ffd6943437503245607820e8951b69f21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841856"
---
# <a name="sr-iov-oids"></a>SR-IOV Oid

シングルルート i/o 仮想化 (SR-IOV) オブジェクト識別子 (Oid) は、SR-IOV インターフェイスをサポートするミニポートおよびそれ以降のドライバーに適用されます。 このインターフェイスは、NDIS バージョン6.30 以降のバージョンでサポートされています。 

次の表は、sr-iov Oid の特性を定義しています。 次の省略形は、テーブルで Oid の特性を指定するために使用されます。

- Q  
OID は、クエリ要求でのみ使用されます。
- S  
OID は、set requests でのみ使用されます。
- M  
OID は、メソッド要求でのみ使用されます。 これらの要求は、セットまたはクエリ操作に対して発行できます。
- ☓  
OID 要求は、ミニポートドライバーではなく、NDIS によって直接処理されます。 ドライバーには、これらの Oid は発行されません。
- P  
OID 要求は、ネットワークアダプターの物理機能 (PF) のミニポートドライバーに対してのみ発行されます。  
PF ドライバーは、これらの Oid をサポートする必要があります。 また、ドライバーは[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**SupportedOidList**メンバーにこれらの oid を [列挙する必要があります。この oid は、ドライバーがの呼び出しの miniportattributes パラメーターに渡します。NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。
- V  
OID 要求は、ネットワークの仮想機能 (VFs) のいずれかのミニポートドライバーに対してのみ発行されます。  
VF ドライバーでは、これらの Oid がサポートされている必要があります。 また、ドライバーは[NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**SupportedOidList**メンバーにこれらの oid を [列挙する必要があります。この oid は、ドライバーがの呼び出しの miniportattributes パラメーターに渡します。NdisMSetMiniportAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。

| 名前                                                                                                 | Q | S | M | ☓ | P | V |
|---                                                                                                   |---|---|---|---|---|---|
| [OID_NIC_SWITCH_ALLOCATE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)           |   |   | ○ |   | ○ |   | 
| [OID_NIC_SWITCH_CREATE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)         |   |   | ○ |   | ○ |   | 
| [OID_NIC_SWITCH_CREATE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)          |   |   | ○ |   | ○ |   |
| [OID_NIC_SWITCH_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-current-capabilities)  | ○ |   |   | ○ |   |   |  
| [OID_NIC_SWITCH_DELETE_SWITCH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)         |   | ○ |   |   | ○ |   |  
| [OID_NIC_SWITCH_DELETE_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)          |   | ○ |   |   | ○ |   | 
| [OID_NIC_SWITCH_ENUM_SWITCHES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)         | ○ |   |   | ○ |   |   |   
| [OID_NIC_SWITCH_ENUM_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)              | ○ |   |   | ○ |   |   |   
| [OID_NIC_SWITCH_ENUM_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)           | ○ |   |   | ○ |   |   |  
| [OID_NIC_SWITCH_FREE_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)               |   | ○ |   |   | ○ |   | 
| [OID_NIC_SWITCH_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-hardware-capabilities) | ○ |   |   | ○ |   |   |   
| [OID_NIC_SWITCH_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)            |   |   | ○ |   | ○ |   | 
| [OID_NIC_SWITCH_VF_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)         |   |   | ○ |   | ○ |   | 
| [OID_NIC_SWITCH_VPORT_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)      |   |   | ○ |   | ○ |   | 
| [OID_SRIOV_BAR_RESOURCES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-bar-resources)              |   | ○ |   |   | ○ |   | 
| [OID_SRIOV_CURRENT_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)       | ○ |   |   | ○ |   |   |   
| [OID_SRIOV_HARDWARE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)      | ○ |   |   | ○ |   |   |   
| [OID_SRIOV_PF_LUID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-pf-luid)                    | ○ |   |   | ○ |   |   |   
| [OID_SRIOV_PROBED_BARS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)                | ○ |   |   |   | ○ |   | 
| [OID_SRIOV_READ_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-block)       |   |   | ○ |   | ○ |   | 
| [OID_SRIOV_READ_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)       |   |   | ○ |   | ○ |   | 
| [OID_SRIOV_RESET_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)                   |   | ○ |   |   | ○ |   | 
| [OID_SRIOV_SET_VF_POWER_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)         |   | ○ |   |   | ○ |   |  
| [OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-invalidate-config-block) |   |   | ○ |   |   | ○ | 
| [OID_SRIOV_VF_SERIAL_NUMBER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-serial-number)           | ○ |   |   | ○ |   |   |   
| [OID_SRIOV_VF_VENDOR_DEVICE_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-vf-vendor-device-id)        |   |   | ○ |   | ○ |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-block)      |   | ○ |   |   | ○ |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)      |   | ○ |   |   | ○ |   |


