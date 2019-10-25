---
title: 仮想関数の電源状態の設定
description: 仮想関数の電源状態の設定
ms.assetid: 7504677D-9B3A-47A2-9990-7BBF50A832EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7846d99bf5b4fa47ba03bb56b3d3c9be10fcd07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841924"
---
# <a name="setting-the-power-state-of-a-virtual-function"></a>仮想関数の電源状態の設定


それより前のドライバーは、Oid のオブジェクト識別子 (OID) セット要求を発行[\_SRIOV\_\_VF\_電源\_状態を設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)して、ネットワークアダプターの指定された PCI Express (PCIe) 仮想関数 (vf) の電源状態を変更します。 電源状態の変更は特権操作であるため、この OID セット要求は、ネットワークアダプターの PCIe 物理機能 (PF) のミニポートドライバーに発行されます。 次に、PF ミニポートドライバーは、指定された電源状態を VF に設定します。

たとえば、仮想化スタックは、VF に接続されている Hyper-v 子パーティションの電源の状態を管理します。 このスタックは、 [\_VF\_電力\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)を PF ミニポートドライバーに\_設定する OID\_SRIOV を発行することによって、電源の状態を変更します。

Oid\_SRIOV の OID セット要求を発行する前に[\_\_vf\_電力\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)を設定する前に、前のドライバーでは、\_VF\_電力\_設定された NDIS\_SRIOV のメンバーを設定する必要があり[ **\_STATE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)構造体は、次のようになります。

-   **VFId**メンバーには、情報の読み取り元となる VF の識別子を設定する必要があります。

-   **PowerState**メンバーは、VF の移行先の電源状態に設定する必要があります。

-   ネットワークアダプターの WAKE\# 信号 (PCI Express バス) または PME\# 信号 (PCI バス上) が低電力状態になったときにアサートされている必要がある場合は、 **WakeEnable**メンバーを TRUE に設定する必要があります。 それ以外の場合は、このメンバーを FALSE に設定する必要があります。

PF ミニポートドライバーがこの OID セット要求を発行するときは、次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された vf\_\_設定されていることを確認する必要があります[**vf\_POWER\_状態\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)構造には、以前のリソースが含まれています。済み. PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)れるため、vf のリソースを割り当てます。 指定した VF が割り当て済みの状態でない場合、ドライバーは OID 要求を失敗させる必要があります。

-   電源状態操作は、指定された VF にのみ影響する必要があります。 この操作は、同じネットワークアダプター上の他の VFs または PF に影響しないようにする必要があります。

 

 





