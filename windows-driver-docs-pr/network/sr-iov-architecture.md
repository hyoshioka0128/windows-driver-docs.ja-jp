---
title: SR-IOV のアーキテクチャ
description: SR-IOV のアーキテクチャ
ms.assetid: 548856F5-823A-4064-A6C3-28CA9FBA3860
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfefc6a1feaf4d441499f78402eb21e05fb730c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551229"
---
# <a name="sr-iov-architecture"></a>SR-IOV のアーキテクチャ


このセクションでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスの概要とそのコンポーネントを提供します。

次の図は、Windows Server 2012 で NDIS 6.30 以降、SR-IOV 対応のコンポーネントを示します。

![親パーティションの管理と、sr-iov アダプターおよびゲスト オペレーティング システムを含む 2 つの子パーティションを示すスタックの図](images/sriovarchitecture.png)

SR-IOV インターフェイスは、次のコンポーネントで構成されます。

<a href="" id="hyper-v-extensible-switch-module"></a>HYPER-V 拡張可能スイッチ モジュール  
NIC を構成する拡張可能スイッチ モジュールは、HYPER-V 子パーティションへのネットワーク接続を提供する、SR-IOV ネットワーク アダプターに切り替えます。

**注**  HYPER-V 子パーティションと呼ばれる*仮想マシン (Vm)* します。

 

子パーティションでに、PCI Express (PCIe) 仮想機能 (VF) を接続している場合は、拡張可能スイッチ モジュールは、VM とネットワーク アダプター間のデータ トラフィックは参加しません。 代わりに、データのトラフィックは、VM とが接続されている VF 間で直接渡されます。

拡張可能スイッチの詳細については、[Hyper-v 拡張可能スイッチ](hyper-v-extensible-switch.md)を参照してください。

<a href="" id="physical-function--pf-"></a>物理機能 (PF)  
PF は、SR-IOV 対応インターフェイスをサポートするネットワーク アダプターの PCI Express (PCIe) 関数です。 PF には、PCIe 構成領域で SR-IOV 対応の拡張機能が含まれています。 機能は、構成および仮想化を有効にして、VFs を公開するなど、ネットワーク アダプターの SR-IOV 機能の管理に使用されます。

詳細については、[SR-IOV 物理機能 (PF)](sr-iov-physical-function--pf-.md)を参照してください。

<a href="" id="pf-miniport-driver"></a>PF ミニポート ドライバー  
PF のミニポート ドライバーが 1 つまたは複数の VFs によって使用されるネットワーク アダプター上のリソースを管理する責任を負います。 このため、すべてのリソースを VF 用に割り当てる前に、管理オペレーティング システムで、PF ミニポート ドライバーが読み込まれます。 VFs に割り当てられたすべてのリソースを解放した後、PF ミニポート ドライバーは停止されます。

詳細については、[書き込み SR-IOV PF ミニポート ドライバー](writing-sr-iov-pf-miniport-drivers.md)を参照してください。

<a href="" id="virtual-function--vf-"></a>仮想機能 (VF)  
VF は、SR-IOV 対応インターフェイスをサポートするネットワーク アダプターで軽量な PCIe 関数です。 VF では、ネットワーク アダプターの VF に関連付けられて、ネットワーク アダプターの仮想化されたインスタンスを表します。 各 VF が、独自の PCI 構成領域です。 各 VF は、PF とその他の VFs も、外部のネットワーク ポートなど、ネットワーク アダプター上の 1 つまたは複数の物理リソースを共有します。

詳細については、[SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)を参照してください。

<a href="" id="vf-miniport-driver"></a>VF ミニポート ドライバー  
VF のミニポート ドライバーは VF を管理する VM にインストールされます。 VF のミニポート ドライバーによって実行されるすべての操作では、その他の任意の VF または同じネットワーク アダプターの PF には影響する必要があります。

詳細については、[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)を参照してください。

<a href="" id="network-interface-card--nic--switch"></a>ネットワーク インターフェイス カード (NIC) のスイッチ  
NIC のスイッチは、SR-IOV 対応インターフェイスをサポートするネットワーク アダプターのハードウェア コンポーネントです。 NIC のスイッチでは、アダプターの物理ポートと内部仮想ポート (拡張) 間のネットワーク トラフィックを転送します。 各 VPort は、PF または、VF のいずれかにアタッチされます。

詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

<a href="" id="virtual-ports--vports-"></a>仮想ポート (拡張)  
VPort は、SR-IOV 対応インターフェイスをサポートするネットワーク アダプターの NIC のスイッチを内部ポートを表すデータ オブジェクトです。 PF または VF ポートが接続されていると、NIC のスイッチ上の VPort 提供パケットを物理スイッチ上のポートと同様に、します。

詳細については、[NIC スイッチ](nic-switches.md)を参照してください。

<a href="" id="physical-port"></a>物理ポート  
物理ポートは、SR-IOV 対応インターフェイスをサポートするネットワーク アダプターのハードウェア コンポーネントです。 物理ポートは、メディアは、外部ネットワーク アダプターのインターフェイスを提供します。

 

 





