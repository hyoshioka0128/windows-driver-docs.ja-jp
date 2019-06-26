---
title: SR-IOV 仮想機能 (VF)
description: SR-IOV 仮想機能 (VF)
ms.assetid: 92EFC8C3-A610-46EB-A1BC-750715378077
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fefb5acf9e4cbc98fa08407150d57b87870cf849
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386206"
---
# <a name="sr-iov-virtual-functions-vfs"></a>SR-IOV 仮想機能 (VF)


PCI Express (PCIe) 仮想機能 (VF) は、ライトウェイト シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターに対して PCIe 関数です。 VF であり、ネットワーク アダプター上 PCIe 物理機能 (PF) と関連付けられているネットワーク アダプターの仮想化されたインスタンスを表します。 各 VF が、独自の PCI 構成領域です。 各 VF は、PF とその他の VFs も、外部のネットワーク ポートなど、ネットワーク アダプター上の 1 つまたは複数の物理リソースを共有します。

VF は本格的な PCIe デバイスではありません。 ただし、HYPER-V 子パーティションと基になる、SR-IOV ネットワーク アダプター間でデータを直接転送するための基本的なメカニズムを提供します。 データ転送に関連付けられているソフトウェアのリソース、VF を直接利用し、は、その他の VFs または、PF. によって使用から分離されます。 ただし、これらのリソースのほとんどの構成は、HYPER-V 親パーティションの管理オペレーティング システムで実行されている PF ミニポート ドライバーで実行されます。

仮想ネットワーク アダプターとして公開される、VF (*VF のネットワーク アダプター*) HYPER-V 子パーティションで実行されているゲスト オペレーティング システムでします。 VF が、SR-IOV ネットワーク アダプターの NIC のスイッチ上の仮想ポート (VPort) に関連付けると、VM で実行されている仮想 PCI (VPCI) ドライバーは VF のネットワーク アダプターを公開します。 公開されると、ゲスト オペレーティング システムでの PnP マネージャーは VF のミニポート ドライバーを読み込みます。

**注**  A HYPER-V 子パーティションとも呼ばれますが、*仮想マシン (VM)* します。

 

VF のミニポート ドライバーは、VF を管理する VM にインストールされている NDIS ミニポート ドライバーです。 VF のミニポート ドライバーによって実行されるすべての操作では、その他の任意の VF または同じネットワーク アダプターの PF には影響する必要があります。

VF のミニポート ドライバーは、PCI デバイス ドライバーのように機能できます。 読み取り/VF の PCI 構成領域に書き込むことができます。 ただし、仮想 PCI デバイスへのアクセスは特権が必要ですし、次のように、PF ミニポート ドライバーによって管理されています。

-   VF のミニポート ドライバーを呼び出すと[ **NdisMGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetbusdata) VF のネットワーク アダプターの PCI 構成領域からデータを読み取る、仮想化スタックが通知されます。 このスタックは、HYPER-V 親パーティションの管理オペレーティング システムで実行されます。 オブジェクト識別子 (OID) のメソッド要求の発行、スタックは、読み取り要求の通知、 [OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)PF をミニポート ドライバー。 読み取るデータがで指定された、 [ **NDIS\_SRIOV\_読み取り\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)OID 要求に含まれている構造体。

    ドライバーは VF PCI 構成領域から、要求されたデータを読み取るし、OID 要求を完了して、データを返します。 このデータは VF のミニポート ドライバーに返されます場合への呼び出し[ **NdisMGetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetbusdata)が完了するとします。

-   VF のミニポート ドライバーを呼び出すと[ **NdisMSetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata) VF のネットワーク アダプターの PCI 構成領域にデータの書き込みに書き込み要求の仮想化スタックに通知します。 OID メソッド要求を発行[OID\_SRIOV\_書き込み\_VF\_CONFIG\_領域](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)PF ミニポート ドライバーにします。 書き込むデータがで指定された、 [ **NDIS\_SRIOV\_書き込み\_VF\_CONFIG\_領域\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)OID 要求に含まれている構造体。

    ドライバーは VF PCI 構成領域にデータを書き込み、OID 要求が完了すると、要求の状態を返します。 この状態は、呼び出しの後 VF のミニポート ドライバーに返される[ **NdisMSetBusData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata)が完了するとします。

VF のミニポート ドライバーも PF ミニポート ドライバーと通信します。 この通信パスは、バック チャネル インターフェイスです。 詳細については、次を参照してください。 [SR-IOV PF/VF のバック チャネル通信](sr-iov-pf-vf-backchannel-communication.md)します。

**注**  VF ミニポート ドライバーは、実行されている仮想化環境内で特定の操作の PF ミニポート ドライバーと通信できるように対応である必要があります。 方法は、ドライバーの詳細については、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

 

 





