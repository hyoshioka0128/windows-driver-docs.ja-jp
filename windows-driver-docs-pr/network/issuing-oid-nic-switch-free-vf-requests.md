---
title: OID_NIC_SWITCH_FREE_VF 要求の発行
description: OID_NIC_SWITCH_FREE_VF 要求の発行
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d56ee45376cc9e3f3a53d424ee08d384bfe1ebf7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356249"
---
# <a name="issuing-oidnicswitchfreevf-requests"></a>OID の発行\_NIC\_スイッチ\_FREE\_VF 要求


上にある、ドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)の PCI Express (PCIe) 仮想機能 (VF) リソースを解放します。 これらのリソースがの OID メソッド要求を通じて割り当てられた以前[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。

上にあるドライバーの問題、 [OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf) PCIe 物理機能 (PF) のミニポート ドライバーに set 要求。 この OID 要求を発行する前に、上にあるドライバー、次の操作する必要があります。

1.  上にあるドライバーでする必要があります、こと、VF にアタッチされていない任意の仮想ポート (VPort) ネットワーク アダプターの NIC のスイッチを確認します。 上にあるドライバーの OID のセット要求を発行する必要があります[OID\_NIC\_スイッチ\_削除\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport) VF に関連付けられているすべての拡張を削除します。 詳細については、次を参照してください。[仮想ポートを削除する](deleting-a-virtual-port.md)します。

2.  上にあるドライバーを初期化します、 [ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)構造体。 ドライバーを設定する必要があります、 **VFId** VF 識別子の OID メソッドの要求で返されたメンバー [OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf).

上にあるドライバーの OID セット要求を発行する[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)次の手順。

1.  上にあるドライバーを初期化します、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID メソッド要求の構造体。 ドライバーのセット、 **InformationBuffer**メンバーが初期化されたへのポインターに[ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)構造体。

2.  上にあるドライバー呼び出し[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)基になる PF ミニポート ドライバーに OID 要求を発行します。

上にある、ドライバーは VF のリソースの割り当てを要求した後、そのドライバーは、同じ VF のリソースの解放が要求できる唯一のコンポーネントになります。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf) VF リソースを解放します。 ドライバーのによって割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)要求。

**注**  上にある、ドライバーがの OID メソッド要求を発行するかどうかは[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)の VF のリソースを割り当てることをドライバーは、同じ VF のリソースの解放が要求できる唯一のコンポーネントです。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf) VF リソースを解放します。 ドライバーの OID で割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に\_NIC\_スイッチ\_ALLOCATE\_VF 要求。

 

 

 





