---
title: 仮想関数のリソースの割り当て
description: 仮想関数のリソースの割り当て
ms.assetid: 00191D2C-E093-4DB7-AC82-8E8E5A74656F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d53fae6f93dccd62de66edfe2be9a7e4f857266
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367720"
---
# <a name="allocating-resources-for-a-virtual-function"></a>仮想関数のリソースの割り当て


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターは、次のハードウェア コンポーネントをサポートできる必要があります。

-   1 つの PCI Express、(PCIe) 物理機能 (PF)。 PF は常にネットワーク アダプターに存在し、HYPER-V 親パーティションにアタッチされます。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 物理機能 (PF)](sr-iov-physical-function--pf-.md)します。

-   1 つまたは複数 PCIe 仮想機能 (VF)。 各 VF は初期化され、ゲスト オペレーティング システムのネットワーク コンポーネントを送信したり、VF 経由のパケットの受信前に、HYPER-V 子パーティションに接続されている必要があります。

    このハードウェア コンポーネントの詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

HYPER-V 親パーティションの管理オペレーティング システムで実行され、PF ミニポート ドライバーでは、PF と各 VF、SR-IOV ネットワーク アダプター上のリソースを割り当てます。 このドライバーでは、任意のネットワーク アダプターの場合と同様に、PF のリソースを割り当てます。 ただし、ドライバーは、次のように各 VF のリソースを割り当てます。

-   PF のミニポート ドライバーは、ドライバーは、ネットワーク アダプターのネットワーク インターフェイス カード (NIC) を作成するときに、各 VF のハードウェア リソースを割り当てます。 ドライバーは、呼び出すことにより、VFs のハードウェア リソースの割り当てを完了[ **NdisMEnableVirtualization**](https://msdn.microsoft.com/library/windows/hardware/hh451481)します。 このプロセスの詳細については、次を参照してください。 [NIC スイッチの作成](creating-a-nic-switch.md)です。

-   PF のミニポート ドライバーでは、ドライバーのオブジェクト識別子 (OID) メソッド要求を処理する際に VF のソフトウェア リソースを割り当てます[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。 場合でも、ハードウェア リソースを VF に対して割り当てられていると見なされる操作不可状態 PF ミニポート ドライバーでは、OID が正常に完了するまで\_NIC\_スイッチ\_ALLOCATE\_VF します。

上にあるドライバーの OID メソッド要求を発行して、VF のソフトウェアのリソースの割り当てを要求できます[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710) OID 要求、へのポインターが含まれている構造体[ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。

OID の要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、ポインター、 [ **NDIS\_NIC\_スイッチ\_VF\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451593)構造体。 この構造体は、アダプター固有の VF 識別子および PCI リクエスター識別子 (RID) を持ちます。 これらの識別子は、次の方法で使用されます。

-   上にあるドライバーは、次など、VF に関連するアクションで VF 識別子を使用します。

    -   現在の VF パラメーターの OID メソッド要求を取得する[OID\_NIC\_スイッチ\_VF\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451824)します。

    -   要求の設定、VF OID を以前に割り当てられたリソースを解放[OID\_NIC\_スイッチ\_FREE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)します。

    -   発行の OID セットの要求を通じて VF にリセット PCI [OID\_SRIOV\_リセット\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)します。

-   RID は、DMA、PF と VF 間割り込み再マップの仮想化スタックで使用されます。 RID は、ハードウェア入出力メモリ管理ユニット (IOMMU) ゲスト物理アドレスをホストの物理アドレスに変換することもできます。

上にあるドライバーの問題の詳細については[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)メソッドの要求を参照してください[発行 OID\_NIC\_スイッチ\_ALLOCATE\_VF 要求](issuing-oid-nic-switch-allocate-vf-requests.md)します。

PF のミニポート ドライバーを処理する方法の詳細については[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)メソッドの要求を参照してください[処理 OID\_NIC\_スイッチ\_ALLOCATE\_VF 要求](handling-oid-nic-switch-allocate-vf-requests.md)します。

**注**  の OID メソッド要求を通じてを VF 用のリソースが割り当てられた後[OID\_NIC\_スイッチ\_ALLOCATE\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)、リソースVF 用のパラメーターは、動的に変更することはできません。

 

 

 





