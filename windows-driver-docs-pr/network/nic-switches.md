---
title: NIC のスイッチ
description: NIC のスイッチ
ms.assetid: 7681DBB2-6645-4B06-9D95-64E7FD379029
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e010a225adcdd610b42d8f523d2e848a4b79362
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530386"
---
# <a name="nic-switches"></a>NIC のスイッチ


シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターはアダプターおよび内部の物理ポート間のネットワーク トラフィックを転送するハードウェアのブリッジを実装する必要があります[仮想ポート (拡張)](virtual-ports--vports-.md)します。 このブリッジと呼ばれる、 *NIC スイッチ*とは、次の図に示します。

![親パーティションの管理と、sr-iov アダプターおよびゲスト オペレーティング システムを含む 2 つの子パーティションを示すスタックの図](images/sriovarchitecture.png)

各 NIC スイッチには、次のコンポーネントが含まれています。

-   1 つの外部または*物理*、外部の物理ネットワークへのネットワーク接続を提供するポート。

-   ネットワーク アダプターで外部の物理ネットワークへのアクセス権を持つ、PCI Express (PCIe) 物理機能 (PF) を提供する 1 つの内部ポート。 内部のポートと呼ばれる、*仮想ポート (VPort)* します。

    PF は、常に作成され、それに割り当てられている VPort を持ちます。 この VPort と呼ばれる、 *VPort の既定*、既定では、参照されている\_VPORT\_ID です。

    拡張の詳細については、次を参照してください。[仮想ポート (拡張)](virtual-ports--vports-.md)します。

-   ネットワーク アダプターで外部の物理ネットワークへのアクセス権を持つ PCIe 仮想機能 (VF) を提供する 1 つまたは複数の拡張。

    **注**  追加の拡張を作成し、ネットワーク アクセスの PF に割り当てられています。

     

**注**  Windows Server 2012 で NDIS 6.30 以降、SR-IOV インターフェイスをサポートしています NIC スイッチが 1 つだけ、ネットワーク アダプター。 このスイッチと呼ばれる、 *NIC スイッチの既定*、NDIS によって参照されている\_既定\_スイッチ\_ID です。

 

NIC のスイッチのハードウェア リソースは、SR-IOV ネットワーク アダプターの PF ミニポート ドライバーによって管理されます。 ドライバーは、作成し、次のメソッドのいずれかで NIC スイッチを構成します。

-   標準化された、SR-IOV と NIC スイッチ INF キーワードに基づく静的作成します。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

-   オブジェクト識別子 (OID) のメソッドの要求ベースの動的な作成[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。 NDIS または HYPER-V 拡張可能スイッチ モジュールは、SR-IOV ネットワーク アダプターに NIC のスイッチを作成するには、これら OID 要求を発行します。

NIC のスイッチを作成、構成、および管理する方法の詳細については、次を参照してください。[管理 NIC スイッチ](managing-nic-switches.md)します。

 

 





