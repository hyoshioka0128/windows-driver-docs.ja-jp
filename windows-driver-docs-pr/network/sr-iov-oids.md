---
title: SR-IOV の Oid
description: このセクションでは、Single Root I/O Virtualization (SR-IOV) の Oid とその特性について説明します。
keywords:
- SR-IOV の Oid
- シングル ルート I/O 仮想化の Oid
- WDK SR-IOV Oid
- SR-IOV オブジェクト識別子
ms.assetid: E93751BF-17BC-4BE7-89F7-53F6C9941120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c197ce76720fb8e67a24355fd260af47f4585b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531143"
---
# <a name="sr-iov-oids"></a>SR-IOV の Oid

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
PF ドライバーは、これらの Oid をサポートする必要があります。 また、ドライバーでこれらの Oid を一覧する必要があります、 **SupportedOidList**のメンバー、 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造で、ドライバーに合格する、 *MiniportAttributes*への呼び出しのパラメーター [NdisMSetMiniportAttributes](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。
- V  
OID 要求は、ネットワークの仮想機能 (Vf) のいずれかのミニポート ドライバーにのみ発行されます。  
VF ドライバーでは、これらの Oid をサポートする必要があります。 また、ドライバーでこれらの Oid を一覧する必要があります、 **SupportedOidList**のメンバー、 [NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES](https://msdn.microsoft.com/library/windows/hardware/ff565923)構造で、ドライバーに合格する、 *MiniportAttributes*への呼び出しのパラメーター [NdisMSetMiniportAttributes](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。

| 名前                                                                                                 | Q | S | M | N | P | V |
|---                                                                                                   |---|---|---|---|---|---|
| [OID_NIC_SWITCH_ALLOCATE_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)           |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_SWITCH](https://msdn.microsoft.com/library/windows/hardware/hh451815)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_CREATE_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)          |   |   | X |   | X |   |
| [OID_NIC_SWITCH_CURRENT_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569760)  | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_DELETE_SWITCH](https://msdn.microsoft.com/library/windows/hardware/hh451817)         |   | X |   |   | X |   |  
| [OID_NIC_SWITCH_DELETE_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)          |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_ENUM_SWITCHES](https://msdn.microsoft.com/library/windows/hardware/hh451819)         | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VFS](https://msdn.microsoft.com/library/windows/hardware/hh451820)              | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_ENUM_VPORTS](https://msdn.microsoft.com/library/windows/hardware/hh451821)           | X |   |   | X |   |   |  
| [OID_NIC_SWITCH_FREE_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)               |   | X |   |   | X |   | 
| [OID_NIC_SWITCH_HARDWARE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569761) | X |   |   | X |   |   |   
| [OID_NIC_SWITCH_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451823)            |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VF_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451824)         |   |   | X |   | X |   | 
| [OID_NIC_SWITCH_VPORT_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh451825)      |   |   | X |   | X |   | 
| [OID_SRIOV_BAR_RESOURCES](https://msdn.microsoft.com/library/windows/hardware/hh451852)              |   | X |   |   | X |   | 
| [OID_SRIOV_CURRENT_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/hh451859)       | X |   |   | X |   |   |   
| [OID_SRIOV_HARDWARE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/hh451862)      | X |   |   | X |   |   |   
| [OID_SRIOV_PF_LUID](https://msdn.microsoft.com/library/windows/hardware/hh451864)                    | X |   |   | X |   |   |   
| [OID_SRIOV_PROBED_BARS](https://msdn.microsoft.com/library/windows/hardware/hh451870)                | X |   |   |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_BLOCK](https://msdn.microsoft.com/library/windows/hardware/hh451874)       |   |   | X |   | X |   | 
| [OID_SRIOV_READ_VF_CONFIG_SPACE](https://msdn.microsoft.com/library/windows/hardware/hh451879)       |   |   | X |   | X |   | 
| [OID_SRIOV_RESET_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)                   |   | X |   |   | X |   | 
| [OID_SRIOV_SET_VF_POWER_STATE](https://msdn.microsoft.com/library/windows/hardware/hh451896)         |   | X |   |   | X |   |  
| [OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK](https://msdn.microsoft.com/library/windows/hardware/hh451903) |   |   | X |   |   | X | 
| [OID_SRIOV_VF_SERIAL_NUMBER](https://msdn.microsoft.com/library/windows/hardware/hh451909)           | X |   |   | X |   |   |   
| [OID_SRIOV_VF_VENDOR_DEVICE_ID](https://msdn.microsoft.com/library/windows/hardware/hh451913)        |   |   | X |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_BLOCK](https://msdn.microsoft.com/library/windows/hardware/hh451918)      |   | X |   |   | X |   | 
| [OID_SRIOV_WRITE_VF_CONFIG_SPACE](https://msdn.microsoft.com/library/windows/hardware/hh451925)      |   | X |   |   | X |   |


