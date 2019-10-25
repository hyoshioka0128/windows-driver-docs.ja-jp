---
title: VF ミニポート ドライバーの初期化
description: VF ミニポート ドライバーの初期化
ms.assetid: 23EB2086-E882-4CB6-A910-D8E99E0212E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac6e759c6e92277324e89f0c91d3d5de265d5d2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824499"
---
# <a name="initializing-a-vf-miniport-driver"></a>VF ミニポート ドライバーの初期化


このトピックでは、PCI Express (PCIe) 仮想機能 (VF) 用のミニポートドライバー用の[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を記述するためのガイドラインについて説明します。 VF は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターによって公開されます。

> [!NOTE]
> これらのガイドラインは、sr-iov ネットワークアダプターの VF ミニポートドライバーにのみ適用されます。 アダプターの PCIe 物理機能 (PF) のミニポートドライバーの初期化ガイドラインについては、「 [Pf ミニポートドライバーの初期化](initializing-a-pf-miniport-driver.md)」を参照してください。 

VF ミニポートドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が呼び出されたときに、NDIS ミニポートドライバーと同じ手順に従います。 これらの手順の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

これらの手順に加えて、NDIS ミニポートドライバーは、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すときに、次の追加の手順に従う必要があります。

- VF ミニポートドライバーは、 [**NdisGetHypervisorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgethypervisorinfo)関数を呼び出して、hyper-v 子パーティションで実行されていることを確認します。 この関数は、パーティションの種類を定義する[**NDIS\_ハイパーバイザー\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hypervisor_info)構造体を返します。 パーティションの種類が**NdisHypervisorPartitionMsHvChild**として報告された場合、ミニポートドライバーは、アダプターの PF に接続されている hyper-v 子パーティションで実行されています。

  > [!NOTE] 
  > パーティションの種類が**NdisHypervisorPartitionMsHvParent**として報告された場合、ミニポートドライバーは、アダプターの PF に接続されている hyper-v の親パーティションで実行されています。 この場合、ミニポートドライバーを VF ドライバーとして初期化することはできません。 可能であれば、ドライバーを PF ドライバーとして初期化する必要があります。詳細については、「 [Pf ミニポートドライバーの初期化シーケンス](initialization-sequence-for-pf-miniport-drivers.md)」を参照してください。     

- PF ミニポートドライバーとは異なり、VF ミニポートドライバーを SR-IOV の標準化されたキーワードと共にインストールすることはできません。また、これらのキーワードを読み取ることはできません。 これらのキーワードの詳細については、「sr-iov の標準化された[INF キーワード](standardized-inf-keywords-for-sr-iov.md)」を参照してください。

- VF ミニポートドライバーは、次の方法で初期化される[**NDIS\_SRIOV\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)の構造を通じて、基になる仮想ネットワークアダプターの sr-iov ハードウェア機能を報告します。

  1. ミニポートドライバーは、**ヘッダー**メンバーを初期化します。 ドライバーは、**ヘッダー**の**type**メンバーを、既定\_\_型の NDIS\_OBJECT に設定します。

     NDIS 6.30 以降では、ミニポートドライバーは、**ヘッダー**の**リビジョン**メンバーを NDIS\_SRIOV\_機能 \_リビジョン\_1、**サイズ**メンバーを ndis\_SIZEOF\_SRIOV に設定\_機能\_REVISION\_1 です。

  2. このミニポートドライバーは、SR-IOV 機能を報告するために、 **SriSRIOV 機能**メンバーで、NDIS\_\_CAP\_PF\_ミニポートフラグを設定します。

     > [!NOTE]
     > VF ミニポートドライバーでは、NDIS\_SRIOV\_CAPS\_VF\_ミニポートフラグと NDIS\_SRIOV\_CAPS\_SRIOV\_supported フラグの両方を設定する必要があります。         

  VF ミニポートドライバーは、次の手順に従って、ネットワークアダプターの SR-IOV 機能を登録します。

  1.  ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)の構造を初期化します。

      ミニポートドライバーは、前に初期化された[**NDIS\_SRIOV\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)構造体へのポインターに、**ハード waresri**のメンバーと**currentsriて**いる機能のメンバーを設定します。

  2.  ドライバーは[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 *miniportattributes*パラメーターを[**NDIS\_ミニポート\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)へのポインターに設定します。\_ハードウェア\_\_属性の構造をサポートします。

- VF ミニポートドライバーでは、仮想マシンキュー (VMQ) 機能をアドバタイズできません。 ただし、ドライバーは、電源管理や receive side scaling (RSS) など、他の NDIS テクノロジのサポートを提供できます。

  RSS の詳細については、「 [Receive Side Scaling](ndis-receive-side-scaling2.md)」を参照してください。

 

 





