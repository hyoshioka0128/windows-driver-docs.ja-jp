---
title: 仮想関数のリソースの割り当て
description: 仮想関数のリソースの割り当て
ms.assetid: 00191D2C-E093-4DB7-AC82-8E8E5A74656F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2716e636670a0593e9a602d8d1226d2862938844
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835297"
---
# <a name="allocating-resources-for-a-virtual-function"></a>仮想関数のリソースの割り当て


シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターは、次のハードウェアコンポーネントをサポートしている必要があります。

-   1つの PCI Express (PCIe) 物理機能 (PF)。 PF は常にネットワークアダプターに存在し、Hyper-v の親パーティションに接続されています。

    このハードウェアコンポーネントの詳細については、「sr-iov[物理機能 (PF)](sr-iov-physical-function--pf-.md)」を参照してください。

-   1つまたは複数の PCIe 仮想関数 (VF)。 各 VF を初期化し、Hyper-v の子パーティションに接続してから、ゲストオペレーティングシステムのネットワークコンポーネントが VF を介してパケットを送受信できるようにする必要があります。

    このハードウェアコンポーネントの詳細については、「 [Sr-iov 仮想機能 (VFs)](sr-iov-virtual-functions--vfs-.md)」を参照してください。

PF ミニポートドライバーは、Hyper-v の親パーティションの管理オペレーティングシステムで実行されます。これにより、SR-IOV ネットワークアダプター上の PF と各 VF のリソースが割り当てられます。 このドライバーは、任意のネットワークアダプターの場合と同様に、PF のリソースを割り当てます。 ただし、ドライバーは、次の方法で各 VF のリソースを割り当てます。

-   PF ミニポートドライバーは、ドライバーがネットワークアダプターにネットワークインターフェイスカード (NIC) を作成するときに、各 VF のハードウェアリソースを割り当てます。 ドライバーは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出すことによって、VFs のハードウェアリソースの割り当てを完了します。 このプロセスの詳細については、「 [NIC スイッチの作成](creating-a-nic-switch.md)」を参照してください。

-   PF ミニポートドライバーは、ドライバーが Oid のオブジェクト識別子 (OID) メソッドの要求を処理するときに、vf のソフトウェアリソースを割り当てます。 [\_NIC\_スイッチによって\_vf が割り当て\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)ます。 ハードウェアリソースが VF に割り当てられている場合でも、PF ミニポートドライバーは、\_VF\_割り当てるために、nonoperational NIC\_スイッチの\_OID を正常に完了するまで、と見なされます。

その後のドライバーは、oid の OID メソッド要求を発行することによって、VF のソフトウェアリソースの割り当てを要求できます。そのためには[\_vf\_割り当てるために、oid\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)を使用します。 OID 要求の[ **\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体へのポインターが含まれています。

OID 要求から正常に返された後、 [**ndis\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、 [**ndis\_NIC\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体へのポインターが含まれています。 この構造体には、アダプター固有の VF 識別子と PCI 要求元識別子 (RID) があります。 これらの識別子は、次の方法で使用されます。

-   この後のドライバーは、次のように、VF に関連するアクションで VF 識別子を使用します。

    -   Oid\_NIC の OID メソッド要求を使用して現在の VF パラメーターを取得する[\_スイッチ\_VF\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。

    -   Oid [\_NIC\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)の oid セット要求を通じて、以前に割り当てられた vf のリソースを解放\_vf\_。

    -   Oid\_oid の設定要求を通じて、VF に PCI リセットを発行すると、 [\_vf\_リセット](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)されます。

-   RID は、仮想化スタックで、PF と VF の間で DMA と割り込みを再マップするために使用されます。 RID を使用すると、ハードウェアの入出力 (memory management unit) を使用して、ゲストの物理アドレスをホストの物理アドレスに変換することもできます。

追加のドライバーが[oid\_nic](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)を発行する方法の詳細については\_スイッチを使用して\_\_vf メソッド要求を割り当てる方法については、「OID\_nic\_の発行」を参照して[\_VF 要求の割り当て](issuing-oid-nic-switch-allocate-vf-requests.md)\_ます。

PF ミニポートドライバーが[oid\_nic](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)を処理する方法の詳細については\_スイッチを使用して\_\_vf メソッド要求を割り当てる方法については、「OID\_NIC の処理」を参照して\_[VF 要求の割り当て](handling-oid-nic-switch-allocate-vf-requests.md)\_ます。\_

\_\_NIC の OID メソッド要求を使用して vf のリソースが割り当てられた後に  、 [\_\_vf の割り当て](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)、vf のリソースパラメーターを動的に変更**することは**できません。

 

 

 





