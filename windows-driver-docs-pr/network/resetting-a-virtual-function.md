---
title: 仮想関数のリセット
description: 仮想関数のリセット
ms.assetid: 4B7A4E02-6383-45FB-9F75-D17C047C40D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1ec9e3385fb7b39720bbea442f0f67fbdc547dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842027"
---
# <a name="resetting-a-virtual-function"></a>仮想関数のリセット


前のドライバーが、指定された PCI Express (PCIe) 仮想関数 (VF) をリセットするために、Oid のオブジェクト識別子 (OID) セット要求を発行[\_SRIOV\_リセット\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf) 。 VF は、シングルルート i/o 仮想化をサポートするネットワークアダプターのハードウェアコンポーネントです。 この OID セット要求は、PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに発行されます。

たとえば、仮想化スタックは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。 スタックは、Hyper-v 子パーティションから VF をデタッチする前に、VF で関数レベルのリセット (FLR) を要求します。 FLR は特権操作であるため、管理オペレーティングシステムでも実行される PF ミニポートドライバーによってのみ実行できます。 指定された VF の FLR を要求するために、仮想化スタックは[OID\_SRIOV\_リセット\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)要求を PF ミニポートドライバーに発行します。

この OID セット要求を発行する前に、前のドライバーは[ **\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)構造体をリセット\_には、NDIS\_SRIOV を初期化する必要があります。 ドライバーは、 **VFId**メンバーをリセットする VF の識別子に設定する必要があります。

この OID 要求を処理するとき、PF ミニポートドライバーは次のガイドラインに従う必要があります。

-   PF ミニポートドライバーは、NDIS\_SRIOV の**VFId**メンバーによって指定された VF [ **\_PARAMETERS 構造\_\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)され、以前に割り当てられたリソースがあることを確認する必要があります。 PF ミニポートドライバーは、oid の OID メソッド要求中に、 [\_NIC\_スイッチによって\_vf\_割り当てら](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)れるため、vf のリソースを割り当てます。 指定された VF のリソースが割り当てられていない場合、ドライバーは OID 要求を失敗させる必要があります。

-   リセット操作は、指定された VF にのみ影響する必要があります。 この操作は、同じネットワークアダプター上の他の VFs または PF に影響しないようにする必要があります。

 

 





