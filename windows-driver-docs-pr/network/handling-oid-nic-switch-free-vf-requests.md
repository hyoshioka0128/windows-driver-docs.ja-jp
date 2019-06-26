---
title: OID_NIC_SWITCH_FREE_VF 要求の処理
description: OID_NIC_SWITCH_FREE_VF 要求の処理
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e919e539b363a2737ce31391f77c6415cead1c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379794"
---
# <a name="handling-oidnicswitchfreevf-requests"></a>OID の処理\_NIC\_スイッチ\_FREE\_VF 要求


PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーがのオブジェクト識別子 (OID) のセット要求を処理するときに[OID\_NIC\_スイッチ\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)は次のこと。

-   **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 要求、へのポインターが含まれている構造体[ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)構造体。 PF のミニポート ドライバーは、ことを確認する必要があります、識別子の PCIe 仮想機能 (VF)、によって指定される、 **VFId**メンバーは有効です。 これが true でない場合、ドライバーでは OID セット要求を NDIS を返すことによって失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF のミニポート ドライバーは VF 用のリソースがの OID メソッド要求を介して以前割り当てられたことを確認する必要があります[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)します。 これが true でない場合、ドライバーでは OID セット要求を NDIS を返すことによって失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF のミニポート ドライバーでは、仮想ポート (拡張) が現在アタッチ VF にされていないことを確認してください。 True でない場合と、ドライバーが NDIS を返すことによってセットの要求を失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF ミニポート ドライバーには、指定した VF に割り当てられたすべてのソフトウェア リソースを解放する必要があります。

-   PF のミニポート ドライバーでは、ネットワーク アダプターで NIC スイッチから VF をデタッチする必要があります。

ドライバーで NDIS OID 要求が完了すると、PF ミニポート ドライバーが正常に割り当てられたソフトウェアのリソースを解放および NIC スイッチから VF をデタッチできる場合、\_状態\_成功します。

**注**  NDIS NDIS の OID セット要求を発行する前に、ミニポートに割り当てられている VFs すべて解放されることを保証[OID\_NIC\_スイッチ\_削除\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch) PF ミニポート ドライバーにします。 この OID を処理する場合、ドライバーは、ネットワーク アダプターで NIC スイッチを削除します。

 

 

 





