---
title: VF ミニポート ドライバーの初期化
description: VF ミニポート ドライバーの初期化
ms.assetid: 23EB2086-E882-4CB6-A910-D8E99E0212E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2911ef3105d352abd0e0383e4ed6746e38f99fd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572488"
---
# <a name="initializing-a-vf-miniport-driver"></a>VF ミニポート ドライバーの初期化


このトピックでは、書き込みのためのガイドラインを説明します、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)ミニポート ドライバーを PCI Express (PCIe) 仮想機能 (VF) の関数。 VF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターによって公開されます。

> [!NOTE]
> 次のガイドラインは、SR-IOV ネットワーク アダプターのミニポート ドライバーを VF にのみ適用されます。 PCIe 物理機能 (PF) アダプターのミニポート ドライバーの初期化ガイドラインについては、次を参照してください。 [PF ミニポート ドライバーの初期化](initializing-a-pf-miniport-driver.md)します。 

VF のミニポート ドライバーが任意の NDIS ミニポート ドライバーと同じ手順に従うときにその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数が呼び出されます。 次の手順の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

この手順に加えて、VF のミニポート ドライバーする必要があります追加の手順に従って NDIS ドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

- VF ミニポート ドライバーの呼び出し、 [ **NdisGetHypervisorInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562635) HYPER-V 子パーティションで実行されていることを確認する関数。 この関数を返します、 [ **NDIS\_ハイパーバイザー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565708)パーティションの種類を定義する構造体。 パーティションの種類として報告される場合**NdisHypervisorPartitionMsHvChild**、ミニポート ドライバーが、アダプターの PF にアタッチされている HYPER-V 子パーティションで実行されています。

  > [!NOTE] 
  > パーティションの種類として報告される場合**NdisHypervisorPartitionMsHvParent**、ミニポート ドライバーが、アダプターの PF にアタッチされている、HYPER-V 親パーティションで実行されています。 この場合、ミニポート ドライバーは VF ドライバーとして初期化しないでください。 」の説明に従って、PF ドライバーとしてに初期化する必要があります、ドライバーの可能な場合は、 [PF ミニポート ドライバーの初期化シーケンス](initialization-sequence-for-pf-miniport-drivers.md)します。     

- PF ミニポート ドライバーとは異なり、VF ミニポート ドライバー、SR-IOV が標準化されているキーワードと共にインストールする必要がある必要がありますしようし、これらのキーワードを読み取る。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

- VF のミニポート ドライバーを通じて基になる仮想ネットワーク アダプターの SR-IOV 対応のハードウェア機能の報告、 [ **NDIS\_SRIOV\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)構造体次のように初期化されます。

  1. ミニポート ドライバーを初期化します、**ヘッダー**メンバー。 ドライバーのセット、**型**のメンバー**ヘッダー** NDIS に\_オブジェクト\_型\_既定します。

     NDIS 6.30 以降、ミニポート ドライバーの設定、**リビジョン**のメンバー**ヘッダー** NDIS に\_SRIOV\_機能\_リビジョン\_1 と**サイズ**NDIS メンバー\_SIZEOF\_SRIOV\_機能\_リビジョン\_1。

  2. ミニポート ドライバーの設定、NDIS\_SRIOV\_CAP\_PF\_ミニポート フラグ、 **SriovCapabilities**レポート、SR-IOV 機能へのメンバー。

     > [!NOTE]
     > VF のミニポート ドライバーは、両方の NDIS を設定する必要があります\_SRIOV\_CAP\_VF\_ミニポート フラグは、NDIS\_SRIOV\_CAP\_SRIOV\_サポートされているフラグ。         

  VF のミニポート ドライバーでは、次の手順に従って、ネットワーク アダプターの SR-IOV 機能を登録します。

  1.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

      ミニポート ドライバーのセット、 **HardwareSriovCapabilities**と**CurrentSriovCapabilities** 、previouslyinitialized へのポインターをメンバー [ **NDIS\_SRIOV\_機能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)構造体。

  2.  ドライバー呼び出し[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)設定と、 *MiniportAttributes*パラメーターへのポインターを[ **NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)構造体。

- VF のミニポート ドライバーは、仮想マシン キュー (VMQ) 機能をアドバタイズしない必要があります。 ただし、ドライバーは、電源管理など、他の NDIS テクノロジのサポートを提供し、受信側 scaling (RSS)。

  RSS の詳細については、次を参照してください。 [Receive Side Scaling](ndis-receive-side-scaling2.md)します。

 

 





