---
title: 仮想関数の電源状態の設定
description: 仮想関数の電源状態の設定
ms.assetid: 7504677D-9B3A-47A2-9990-7BBF50A832EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 638eaa417f3071171511f719491b4f21abcdbe4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553137"
---
# <a name="setting-the-power-state-of-a-virtual-function"></a>仮想関数の電源状態の設定


上位のドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_SRIOV\_設定\_VF\_POWER\_状態](https://msdn.microsoft.com/library/windows/hardware/hh451896)指定 PCI の電源の状態を変更するにはExpress、ネットワーク アダプターでは、(PCIe) 仮想機能 (VF) を使用します。 電源状態の変更が特権が必要であるために、上にあるドライバーは、ネットワーク アダプターの PCIe 物理機能 (PF) のミニポート ドライバーにこの OID のセット要求を発行します。 PF のミニポート ドライバー、VF で指定された電源の状態を設定します。

たとえば、仮想化スタックは、VF に関連付けられている HYPER-V 子パーティションの電源の状態を管理します。 スタックでは、電源状態を変更を発行して、 [OID\_SRIOV\_設定\_VF\_POWER\_状態](https://msdn.microsoft.com/library/windows/hardware/hh451896)PF ミニポート ドライバーにします。

OID のセット要求を発行する前に[OID\_SRIOV\_設定\_VF\_POWER\_状態](https://msdn.microsoft.com/library/windows/hardware/hh451896)、上にあるドライバーがのメンバーを設定する必要があります[ **NDIS\_SRIOV\_設定\_VF\_POWER\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451683)次のように構造体。

-   **VFId**メンバーは、元の情報が読み取られる VF の識別子を設定する必要があります。

-   **PowerState**メンバーは、VF に移行する必要がある電源状態を設定する必要があります。

-   ネットワーク アダプターにそのウェイク必要がある場合\#(Pci バス) 上のシグナルまたは PME\# 、低電力状態になるようにアサート (PCI バス) でのシグナル、 **WakeEnable**メンバーは、TRUE に設定する必要があります。 それ以外の場合、このメンバーは、FALSE に設定する必要があります。

PF ミニポート ドライバーには、この OID セットの要求が発行される、次のガイドラインに従う必要があります。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_設定\_VF\_POWER\_状態\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451683)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。 割り当てられた状態で指定された VF でない場合、ドライバーは OID 要求に失敗する必要があります。

-   電源状態の操作は、指定 VF のみに影響する必要があります。 操作では、その他の VFs または同じネットワーク アダプターの PF には影響する必要があります。

 

 





