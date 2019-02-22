---
title: 仮想関数をリセットします。
description: 仮想関数をリセットします。
ms.assetid: 4B7A4E02-6383-45FB-9F75-D17C047C40D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a74f7e369b87d4e4ca7d84d4eeea501e007c025
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552680"
---
# <a name="resetting-a-virtual-function"></a>仮想関数をリセットします。


上位のドライバーのオブジェクト識別子 (OID) セット要求を発行する[OID\_SRIOV\_リセット\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)を指定された PCI Express (PCIe) 仮想機能 (VF) をリセットします。 VF とは、シングル ルート I/O 仮想化をサポートするネットワーク アダプターのハードウェア コンポーネントです。 上にあるドライバーは、ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) をこの OID セット要求を発行します。

たとえば、仮想化スタックは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。 スタック、VF HYPER-V 子パーティションから切り離すと、前に、関数レベルのリセット (FLR) で、VF を要求します。 FLR は、特権が必要であるために、管理オペレーティング システムでも実行している PF ミニポート ドライバーによってのみ実行できます。 指定した VF、仮想化スタックに関する問題の FLR を要求する、 [OID\_SRIOV\_リセット\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)PF ミニポート ドライバーに要求します。

この OID セット要求を発行して、前に、上にあるドライバーを初期化する必要があります、 [ **NDIS\_SRIOV\_リセット\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451682)構造体。 ドライバーを設定する必要があります、 **VFId**をリセットする VF の識別子にメンバー。

この OID 要求を処理する場合、PF ミニポート ドライバーは次のガイドラインに従います。

-   PF のミニポート ドライバーは、VF がで指定されたを確認する必要があります、 **VFId**のメンバー、 [ **NDIS\_SRIOV\_リセット\_VF\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451682)構造体を以前に割り当てられているリソースします。 PF のミニポート ドライバーを VF 用のリソースの割り当ての OID メソッド要求中に[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。 指定した VF 用のリソースが割り当てられていない場合、ドライバーは OID 要求に失敗する必要があります。

-   リセット操作には、指定 VF のみ影響する必要があります。 操作では、その他の VFs または同じネットワーク アダプターの PF には影響する必要があります。

 

 





