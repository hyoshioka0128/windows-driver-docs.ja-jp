---
title: Sr-iov 仮想機能 (VFs)
description: Sr-iov 仮想機能 (VFs)
ms.assetid: 92EFC8C3-A610-46EB-A1BC-750715378077
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ba27490b428426b9766c2f98db632896290a58
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841854"
---
# <a name="sr-iov-virtual-functions-vfs"></a>Sr-iov 仮想機能 (VFs)


PCI Express (PCIe) 仮想関数 (VF) は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプター上の軽量の PCIe 機能です。 VF はネットワークアダプターの PCIe 物理機能 (PF) に関連付けられており、ネットワークアダプターの仮想化インスタンスを表します。 各 VF には、独自の PCI 構成領域があります。 また、各 VF は、外部ネットワークポートなど、ネットワークアダプター上の1つ以上の物理リソースを、PF とその他の VFs と共有します。

VF は、本格的な PCIe デバイスではありません。 ただし、Hyper-v の子パーティションと、基になる SR-IOV ネットワークアダプターとの間でデータを直接転送するための基本的なメカニズムが用意されています。 データ転送に関連付けられたソフトウェアリソースは、VF で直接使用でき、他の VFs や PF によって使用されないように分離されています。 ただし、これらのリソースのほとんどの構成は、Hyper-v の親パーティションの管理オペレーティングシステムで実行される PF ミニポートドライバーによって実行されます。

VF は、Hyper-v 子パーティションで実行されるゲストオペレーティングシステムの仮想ネットワークアダプター (*vf ネットワークアダプター*) として公開されます。 SR-IOV ネットワークアダプターの NIC スイッチの仮想ポート (VPort) に VF が関連付けられると、VM で実行される仮想 PCI (VPCI) ドライバーが VF ネットワークアダプターを公開します。 公開されると、ゲストオペレーティングシステムの PnP マネージャーによって、VF ミニポートドライバーが読み込まれます。

Hyper-v 子パーティションは*仮想マシン (VM)* とも呼ばれます  に**注意**してください。

 

VF ミニポートドライバーは、VF を管理するために VM にインストールされる NDIS ミニポートドライバーです。 VF ミニポートドライバーによって実行される操作は、同じネットワークアダプター上の他の VF または PF に影響しないようにする必要があります。

VF ミニポートドライバーは、PCI デバイスドライバーと同様に機能することができます。 VF の PCI 構成領域に対して読み取りと書き込みを行うことができます。 ただし、仮想 PCI デバイスへのアクセスは特権操作であり、次の方法で PF ミニポートドライバーによって管理されます。

-   VF ミニポートドライバーが[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)を呼び出して、vf ネットワークアダプターの PCI 構成領域からデータを読み取ると、仮想化スタックに通知されます。 このスタックは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。 スタックに読み取り要求が通知されると、オブジェクト識別子 (OID) メソッドの Oid\_SRIOV\_が発行されます。この要求は、 [\_VF\_CONFIG\_SPACE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)を PF ミニポートドライバーに読み取ります。 読み取り対象のデータは、OID 要求に含まれている[ **\_VF\_CONFIG\_SPACE\_PARAMETERS 構造\_\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)に指定されています。

    ドライバーは、要求されたデータを VF PCI 構成領域から読み取り、OID 要求を完了することによってデータを返します。 [**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)の呼び出しが完了すると、このデータが VF ミニポートドライバーに返されます。

-   VF ミニポートドライバーが[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)を呼び出して、vf ネットワークアダプターの PCI 構成領域にデータを書き込むときに、仮想化スタックに書き込み要求が通知されます。 Oid\_oid の OID メソッド要求を発行し、 [\_VF\_CONFIG\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)を PF ミニポートドライバーに書き込みます。 書き込まれるデータは、OID 要求に含まれている[ **\_VF\_CONFIG\_\_の構造を書き込む\_\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)に指定されています。

    ドライバーは、データを VF PCI 構成領域に書き込み、OID 要求の完了時に要求の状態を返します。 この状態は、 [**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)の呼び出しが完了した後に、VF ミニポートドライバーに返されます。

VF ミニポートドライバーは、PF ミニポートドライバーとも通信できます。 この通信パスは、backchannel インターフェイスを超えています。 詳細については、「sr-iov [PF/VF バックチャネル通信](sr-iov-pf-vf-backchannel-communication.md)」を参照してください。

VF ミニポートドライバーは、特定の操作のために PF ミニポートドライバーと通信できるように、仮想化された環境で実行されていることを認識している必要が**あり  。** ドライバーがこれを行う方法の詳細については、「 [VF ミニポートドライバーの初期化](initializing-a-vf-miniport-driver.md)」を参照してください。

 

 

 





