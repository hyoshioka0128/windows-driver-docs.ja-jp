---
title: OID_NIC_SWITCH_ALLOCATE_VF 要求の処理
description: OID_NIC_SWITCH_ALLOCATE_VF 要求の処理
ms.assetid: B48A19D5-A768-4614-961D-1BD00762B6D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb57adb84e62e15812e16ee401e2e9d6d0a94558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842584"
---
# <a name="handling-oid_nic_switch_allocate_vf-requests"></a>OID\_NIC の処理\_スイッチ\_\_VF 要求の割り当て


ネットワークアダプター上の PCI Express (PCIe) 物理機能 (PF) のミニポートドライバーが、Oid のオブジェクト識別子 (OID) メソッドの要求を処理するときに、 [\_NIC\_スイッチによって\_VF に割り当て\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)、次の処理が行われます。

-   PF ミニポートドライバーは、ネットワークアダプターに、PCIe 仮想機能 (VF) のソフトウェアリソースを割り当てます。 これらのリソースは、 [**NDIS\_NIC\_スイッチ\_VF\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体で指定されたパラメーターに基づいて構成されます。

-   PF ミニポートドライバーは、ネットワークアダプターの NIC スイッチに VF を割り当てます。 NIC スイッチは、 [**NDIS\_nic\_スイッチ\_VF\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体の**switchid**メンバーによって識別されます。

    NIC スイッチの詳細については、「 [Nic スイッチ](nic-switches.md)」を参照してください。

-   PF ミニポートドライバーは、VF 識別子を使用して**VFId**メンバーを更新します。 この識別子は、0から始まるインデックスであり、PF ミニポートドライバーによって NIC スイッチに割り当てられているすべての VFs で一意である必要があります。

    この後のドライバーは、 [oid\_nic\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)の連続した oid 要求で、 **VFId**メンバーの値を使用して\_\_vf または[oid\_NIC\_スイッチ\_の vf\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)を解放します。

-   PF ミニポートドライバーは、VF の PCIe 要求識別子 (RID) を使用して**RequestorId**メンバーを更新します。

    ミニポートドライバーは、 [**NdisMGetVirtualFunctionLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionlocation)を呼び出して、VF に対応する RID 情報を取得します。 次に、 **NdisMGetVirtualFunctionLocation**への呼び出しによって返された情報に基づいて、 [**NDIS\_MAKE\_rid**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)マクロを使用して、rid を作成します。

    RID は、仮想化スタックで、PF と VF の間で DMA と割り込みを再マップするために使用されます。 RID を使用すると、ハードウェアの入出力 (memory management unit) を使用して、ゲストの物理アドレスをホストの物理アドレスに変換することもできます。

-   PF ミニポートドライバーは、VF を初期化して公開します。 これにより、仮想化スタックで使用できるように VF が準備されます。

PF ミニポートドライバーが必要なソフトウェアリソースを正常に割り当てて、VF を初期化できる場合、ドライバーは NDIS\_STATUS\_SUCCESS を使用して OID 要求を完了します。 PF ミニポートドライバーは、割り当てられた各 VF の VF Id を保持する必要があります。 NDIS およびそれ以降のドライバーでは、VF のリセットや解放などのさまざまな操作のために、PF ミニポートドライバーに対する一連の OID 要求で VF 識別子を使用します。

**  vf**のリソースが割り当てられている場合、vf は接続されていない状態になります。これは、仮想ポート (vport) が vf にアタッチされていないためです。 この後のドライバーは、oid\_の oid 要求を発行できます。 [\_スイッチは\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)を作成して、VF に vport を接続\_ます。 詳細については、「[仮想ポートの作成](creating-a-virtual-port.md)」を参照してください。

 

 

 





