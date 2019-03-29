---
title: OID_NIC_SWITCH_FREE_VF 要求の処理
description: OID_NIC_SWITCH_FREE_VF 要求の処理
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014b2843f9004fe81a1a56200cd3e1f0c52e2692
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572170"
---
# <a name="handling-oidnicswitchfreevf-requests"></a>OID の処理\_NIC\_スイッチ\_FREE\_VF 要求


PCI Express (PCIe) 物理機能 (PF) ネットワーク アダプターのミニポート ドライバーがのオブジェクト識別子 (OID) のセット要求を処理するときに[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)は次のこと。

-   **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID 要求、へのポインターが含まれている構造体[ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451579)構造体。 PF のミニポート ドライバーは、ことを確認する必要があります、識別子の PCIe 仮想機能 (VF)、によって指定される、 **VFId**メンバーは有効です。 これが true でない場合、ドライバーでは OID セット要求を NDIS を返すことによって失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF のミニポート ドライバーは VF 用のリソースがの OID メソッド要求を介して以前割り当てられたことを確認する必要があります[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。 これが true でない場合、ドライバーでは OID セット要求を NDIS を返すことによって失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF のミニポート ドライバーでは、仮想ポート (拡張) が現在アタッチ VF にされていないことを確認してください。 True でない場合と、ドライバーが NDIS を返すことによってセットの要求を失敗する必要があります\_状態\_無効な\_パラメーター。

-   PF ミニポート ドライバーには、指定した VF に割り当てられたすべてのソフトウェア リソースを解放する必要があります。

-   PF のミニポート ドライバーでは、ネットワーク アダプターで NIC スイッチから VF をデタッチする必要があります。

ドライバーで NDIS OID 要求が完了すると、PF ミニポート ドライバーが正常に割り当てられたソフトウェアのリソースを解放および NIC スイッチから VF をデタッチできる場合、\_状態\_成功します。

**注**  NDIS NDIS の OID セット要求を発行する前に、ミニポートに割り当てられている VFs すべて解放されることを保証[OID\_NIC\_スイッチ\_削除\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451817) PF ミニポート ドライバーにします。 この OID を処理する場合、ドライバーは、ネットワーク アダプターで NIC スイッチを削除します。

 

 

 





