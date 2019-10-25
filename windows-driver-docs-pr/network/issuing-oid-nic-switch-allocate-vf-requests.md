---
title: OID_NIC_SWITCH_ALLOCATE_VF 要求の発行
description: OID_NIC_SWITCH_ALLOCATE_VF 要求の発行
ms.assetid: 72285E72-DEC7-4578-9B6C-E616FECD6F41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 619f0f31f651afecfd2258909c79b4eb49396ce7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844153"
---
# <a name="issuing-oid_nic_switch_allocate_vf-requests"></a>OID\_NIC を発行して\_VF 要求を割り当てる\_\_スイッチ


Oid\_のオブジェクト識別子 (OID) メソッド要求を発行する前に、 [NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)によって\_VF を PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーに割り当てる\_、それまでのドライバーは NDIS をフォーマットし[ **\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体です。 この構造体には、ネットワークアダプターの PCIe 仮想機能 (VF) に割り当てられるリソースの構成パラメーターが含まれています。 このようなドライバーでは、次のように、この構造体のメンバーを設定する必要があります。

-   **Switchid**メンバーは、ネットワークアダプターで以前に作成された NIC スイッチの識別子に設定する必要があります。 NIC スイッチを作成するには、oid の oid メソッド要求[oid\_nic\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)を使用します。

    Oid\_\_スイッチの oid メソッド要求を処理するときに[\_vf\_割り当てる](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)と、PCIe 物理機能 (PF) のミニポートドライバーによって、vf のリソースが割り当てられます。 リソースが正常に割り当てられると、PF ミニポートドライバーは、指定された NIC スイッチに VF を割り当てます。

    **メモ** Windows Server 2012 の NDIS 6.30 以降では、SR-IOV インターフェイスはネットワークアダプターの既定の NIC スイッチのみをサポートしています。 **Switchid**メンバーの値は、NDIS\_既定\_スイッチ\_ID に設定する必要があります。

    NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

-   **VFId**メンバーは、\_VF\_関数\_ID\_無効な場合に、NDIS に設定する必要があります。

-   **RequestorId**メンバーを NDIS\_無効\_RID に設定する必要があります。

-   **Vmfriendlyname**メンバーと**VMName**メンバーは、hyper-v 子パーティションのパラメーターに設定する必要があります。 PF ミニポートドライバーは、情報提供の目的でのみこれらのメンバーを使用します。

    **メモ** Hyper-v の子パーティションは、*仮想マシン (VM)* とも呼ばれます。

    VF は、指定された VM に関連付けられてから、\_スイッチ要求を作成\_ために、その後のドライバーが[OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)に発行します。

-   **NicName**メンバーは、仮想マシン (VM) ネットワークアダプターの識別子に設定する必要があります。 この仮想アダプターは、VM で実行されるゲストオペレーティングシステムで公開されます。 PF ミニポートドライバーは、情報提供のみを目的としてこのメンバーを使用します。

    VF にリソースが割り当てられ、子パーティションに接続されている場合、VF ネットワークアダプターはゲストオペレーティングシステムで公開されます。 VM ネットワークアダプターは、ハードウェアベースの VF データパスを経由したパケット転送用の VF ネットワークアダプターをチームにします。

    ただし、ライブマイグレーション中など、子パーティションから VF をデタッチすることもできます。 この場合、パケット転送はソフトウェアベースの合成データパスを介して行われます。 これらのデータパスの詳細については、「sr-iov[データパス](sr-iov-data-paths.md)」を参照してください。

-   **PermanentMacAddress**および**currentmacaddress**メンバーは、VF の仮想ネットワークアダプターのメディアアクセス制御 (MAC) アドレスに設定されている必要があります。 これらのアドレスは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されているネットワークスタックに公開されます。

次の手順に従って、その後のドライバーが oid\_\_oid の oid メソッド要求を発行し、 [\_VF\_割り当てる](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ことができます。

1.  前のドライバーは、OID メソッド要求の[**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造を初期化します。 ドライバーは、初期化された[**NDIS\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体へのポインターに**informationbuffer**メンバーを設定します。

2.  前のドライバーは、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、基になる PF ミニポートドライバーに OID 要求を発行します。

    **メモ** 前のドライバーが[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出すと、NDIS は OID 要求をインターセプトし、 [**ndis\_NIC\_スイッチ\_vf\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体に指定されている vf パラメーターを検証します。 パラメーターが正常に検証された場合、NDIS は、その OID を PF ミニポートドライバーに転送します。 それ以外の場合、NDIS は NDIS\_STATUS の OID 要求\_無効な\_パラメーターを使用して失敗します。

あるドライバーが VF のリソース割り当てを要求した後、そのドライバーは、同じ VF のリソースの解放を要求できる唯一のコンポーネントです。 この後のドライバーは、oid\_NIC の OID セット要求を発行する必要があります。これは、 [\_空き\_vf の\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)によって、vf リソースが解放されます。 前のドライバーを停止する前に、ドライバーの[OID\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)によって割り当てられた各 vf のリソースを解放して\_VF 要求の割り当て\_する必要があります。