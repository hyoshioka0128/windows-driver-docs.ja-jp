---
title: OID_NIC_SWITCH_FREE_VF 要求の発行
description: OID_NIC_SWITCH_FREE_VF 要求の発行
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec6849b658de7b791621e1d112a502d4c17e049
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352953"
---
# <a name="issuing-oidnicswitchfreevf-requests"></a>OID の発行\_NIC\_スイッチ\_FREE\_VF 要求


上にある、ドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)の PCI Express (PCIe) 仮想機能 (VF) リソースを解放します。 これらのリソースがの OID メソッド要求を通じて割り当てられた以前[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。

上にあるドライバーの問題、 [OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822) PCIe 物理機能 (PF) のミニポート ドライバーに set 要求。 この OID 要求を発行する前に、上にあるドライバー、次の操作する必要があります。

1.  上にあるドライバーでする必要があります、こと、VF にアタッチされていない任意の仮想ポート (VPort) ネットワーク アダプターの NIC のスイッチを確認します。 上にあるドライバーの OID のセット要求を発行する必要があります[OID\_NIC\_スイッチ\_削除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818) VF に関連付けられているすべての拡張を削除します。 詳細については、次を参照してください。[仮想ポートを削除する](deleting-a-virtual-port.md)します。

2.  上にあるドライバーを初期化します、 [ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451579)構造体。 ドライバーを設定する必要があります、 **VFId** VF 識別子の OID メソッドの要求で返されたメンバー [OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814).

上にあるドライバーの OID セット要求を発行する[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)次の手順。

1.  上にあるドライバーを初期化します、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID メソッド要求の構造体。 ドライバーのセット、 **InformationBuffer**メンバーが初期化されたへのポインターに[ **NDIS\_NIC\_スイッチ\_FREE\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451579)構造体。

2.  上にあるドライバー呼び出し[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)基になる PF ミニポート ドライバーに OID 要求を発行します。

上にある、ドライバーは VF のリソースの割り当てを要求した後、そのドライバーは、同じ VF のリソースの解放が要求できる唯一のコンポーネントになります。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822) VF リソースを解放します。 ドライバーのによって割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)要求。

**注**  上にある、ドライバーがの OID メソッド要求を発行するかどうかは[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)の VF のリソースを割り当てることをドライバーは、同じ VF のリソースの解放が要求できる唯一のコンポーネントです。 上にあるドライバーの OID セット要求を発行する必要があります[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822) VF リソースを解放します。 ドライバーの OID で割り当てられた各 VF のリソースを解放する必要があります上にあるドライバーを停止できますが、前に\_NIC\_スイッチ\_ALLOCATE\_VF 要求。

 

 

 





