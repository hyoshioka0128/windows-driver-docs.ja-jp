---
title: VMQ コンポーネント
description: VMQ コンポーネント
ms.assetid: 74BFE4C1-89C2-400D-A915-88552C215251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20641a8518a111dc8202b5bf61b3e281bdfaf54a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549888"
---
# <a name="vmq-components"></a>VMQ コンポーネント





次の図は、運用環境に仮想マシン キュー (VMQ) で、さまざまなコンポーネント間の関係を示します。

![vmq コンポーネント](images/vmqarch.png)

上記の図は、次の VMQ コンポーネントを示しています。

<a href="" id="--------network-virtual-service-provider--netvsp-"></a> **ネットワークの仮想サービス プロバイダー (NetVSP)**  
HYPER-V 親パーティションの管理オペレーティング システムで実行されている NDIS ドライバー。 このドライバーは、HYPER-V 子パーティションでネットワーク アクセスをサポートするためにサービスを提供します。

**注**  以降 Windows Server 2008 では、HYPER-V 拡張可能スイッチのコンポーネントは、ゲスト オペレーティング システムで実行される NetVSC コンポーネント NetVSP サポートを提供します。 このコンポーネントの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)します。

 

<a href="" id="network-virtual-service-client--netvsc-"></a>**ネットワークの仮想サービス クライアント (NetVSC)**  
HYPER-V 子パーティションのゲスト オペレーティング システムで実行されている NDIS ドライバー。 NetVSC では、物理ネットワーク アダプターのホスト コンピューター上の仮想化されたビューを公開します。 この仮想化されたデバイスと呼ばれる、 *VM ネットワーク アダプター*します。

NetVSC は、次の機能を提供します。

-   ネットワーク、HYPER-V 子パーティションでのデバイス機能をサポートします。

-   関連付けられている NetVSP ドライバーには、仮想マシン バス (VMBus) 経由でメッセージを渡すことによって、物理ネットワーク アダプターにアクセスします。 このドライバーは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。

<a href="" id="--------virtual-machine-bus--------vmbus-"></a> **仮想マシン バス (VMBus)**  
パーティション間で HYPER-V の親と子コントロールとデータのメッセージを通過する仮想通信バスです。

**注**  で、HYPER-V 子パーティションは、仮想マシン (VM) でとも呼ばれます。

 

<a href="" id="vm-bus-channel"></a>**VM バス チャネル**  
HYPER-V 子パーティションでの NetVSC と、HYPER-V 親パーティションで NetVSP 間 VMBus に通信チャネルです。

<a href="" id="vm-queue"></a>**VM のキュー**  
受信したデータのキューです。 VMQ をサポートするネットワーク アダプターには、VM のキューにデータをルーティングするハードウェアがあります。

<a href="" id="vmq-filter"></a>**VMQ フィルター**  
受信データをテストするフィルター。 VMQ をサポートするネットワーク アダプターでは、フィルターを使って、パケットをキューに割り当てるには、パケット データをテストします。

 

 





