---
title: OID_NIC_SWITCH_ALLOCATE_VF 要求の処理
description: OID_NIC_SWITCH_ALLOCATE_VF 要求の処理
ms.assetid: B48A19D5-A768-4614-961D-1BD00762B6D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0747c583201d36e85604d2e520f67ac8659a3ec1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379803"
---
# <a name="handling-oidnicswitchallocatevf-requests"></a>OID の処理\_NIC\_スイッチ\_ALLOCATE\_VF 要求


PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーでのオブジェクト識別子 (OID) メソッド要求を処理するときに[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)は次のこと。

-   PF のミニポート ドライバーでは、PCIe 仮想機能 (VF) ネットワーク アダプターのソフトウェアのリソースを割り当てます。 これらのリソースがで指定したパラメーターに基づいて構成されている、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。

-   PF のミニポート ドライバーでは、ネットワーク アダプター上の NIC スイッチに、VF を割り当てます。 NIC のスイッチがで識別される、 **SwitchId**のメンバー、 [ **NDIS\_NIC\_切り替える\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)構造体。

    NIC のスイッチの詳細については、次を参照してください。 [NIC スイッチ](nic-switches.md)します。

-   PF ミニポート ドライバーの更新プログラム、 **VFId** VF 識別子を持つメンバー。 この識別子は割り当てられているすべての VFs で一意である必要があります、0 から始まるインデックス、PF ミニポート ドライバーによって NIC スイッチ。

    上にあるドライバーの値を使用して、 **VFId**の連続する OID 要求内のメンバー [OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)または[OID\_NIC\_スイッチ\_VF\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)します。

-   PF ミニポート ドライバーの更新プログラム、 **RequestorId**メンバー VF の PCIe リクエスター識別子 (RID) とします。

    ミニポート ドライバー呼び出し[ **NdisMGetVirtualFunctionLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetvirtualfunctionlocation) VF に対応する RID の情報を取得します。 ドライバーを使用して、RID は、 [ **NDIS\_ように\_RID** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)への呼び出しによって返される情報に基づいてマクロ**NdisMGetVirtualFunctionLocation**します。

    RID は、DMA、PF と VF 間割り込み再マップの仮想化スタックで使用されます。 RID は、ハードウェア入出力メモリ管理ユニット (IOMMU) ゲスト物理アドレスをホストの物理アドレスに変換することもできます。

-   PF のミニポート ドライバーを初期化し、VF を公開します。 これにより、仮想化スタックによって VF を使用できる状態にします。

ドライバーで NDIS OID 要求が完了すると、PF ミニポート ドライバーが正常に必要なソフトウェア リソースを割り当てるおよび VF を初期化できる場合、\_状態\_成功します。 PF のミニポート ドライバーでは、割り当てられた各 VF の VF Id を保持する必要があります。 NDIS および上にあるドライバーは、PF ミニポート ドライバーに連続する OID 要求で VF 識別子を使用してリセットや、VF の解放などのさまざまなアクション。

**注**  VF は接続されていない状態で、VF 用のリソースが割り当てられると、仮想ポート (VPort) が、VF にアタッチされていないためです。 上にあるドライバーの OID 要求を発行できる[OID\_NIC\_スイッチ\_作成\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)を作成して、VPort を VF にアタッチします。 詳細については、次を参照してください。[仮想ポートを作成する](creating-a-virtual-port.md)します。

 

 

 





