---
title: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
description: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
ms.assetid: 338035E7-7677-49FE-A06D-CCFD813B0C10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b19b82c301bf078459699dbbe253f93c1af040f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577975"
---
# <a name="miniportinitializeex-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの MiniportInitializeEx ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、[VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)を参照してください。

 

PF のミニポート ドライバーが任意の NDIS ミニポート ドライバーと同じ手順に従うときにその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 次の手順の詳細については、[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)を参照してください。

次の手順に加え、PF ミニポート ドライバーする必要があります追加の手順に従って NDIS ドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

1.  PF のミニポート ドライバー呼び出し、 [ **NdisGetHypervisorInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562635)関数を HYPER-V 親パーティションで実行されていることを確認します。 この関数を返します、 [ **NDIS\_ハイパーバイザー\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565708)パーティションの種類を定義する構造体。 パーティションの種類として報告される場合**NdisHypervisorPartitionMsHvParent**、ミニポート ドライバーが、アダプターの PF にアタッチされている、HYPER-V 親パーティションで実行されています。

    **注**  として、パーティションの種類が報告された場合**NdisHypervisorPartitionMsHvChild**、ミニポート ドライバーが、アダプターの VF に関連付けられている HYPER-V 子パーティションで実行されています。 この場合は、PF ドライバーとしてミニポート ドライバーが初期化しないでください。 」の説明に従って、VF ドライバーとしてに初期化する必要があります、ドライバーの可能な場合は、 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

     

2.  PF のミニポート ドライバーは、SR-IOV が標準化されているキーワード、SR-IOV が有効になっているかどうかを判断し、構成設定を取得するには、NIC のスイッチを読み取る必要があります。 これらのキーワードの詳細については、[SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)を参照してください。

    **注**  PF ミニポート ドライバーのエントリ ポイントが登録されているかどうか、 [ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数の場合、ドライバーが以前に取得からこれらの設定、NDIS が呼び出されたときに、レジストリ*MiniportSetOptions*します。

     

3.  ネットワーク アダプターでは、SR-IOV、仮想マシン キュー (VMQ) または RSS をサポートする場合、ミニポート ドライバーする必要があります、ネットワーク アダプターを有効にするには、どの機能を決定します。 これを確認する方法の詳細については、[処理、SR-IOV、VMQ、および RSS の標準化された INF キーワード](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)を参照してください。

4.  RSS および VMQ のハードウェアの機能 (サポートされている) 場合、と共に、ミニポート ドライバーは、ハードウェア、SR-IOV 機能の完全なセットを報告する必要があります。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ネットワーク アダプターで SR-IOV が有効な場合、ミニポート ドライバーする必要があります、アダプターで現在 SR-IOV 設定がレポートも。

    レポートの SR-IOV 機能の詳細については、[SR-IOV 機能を決定する](determining-sr-iov-capabilities.md)を参照してください。

5.  ミニポート ドライバーには、そのハードウェア NIC スイッチ機能の完全なセットをレポートする必要があります。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ネットワーク アダプターで SR-IOV が有効な場合、ミニポート ドライバーする必要があります、アダプターで現在 NIC スイッチの設定がレポートも。

    スイッチ、NIC をレポート作成の詳細についてを参照してください[NIC スイッチ機能を決定する](determining-nic-switch-capabilities.md)します。

6.  ミニポート ドライバーがその全を報告する必要がありますのハードウェアのセットがフィルター処理機能を受信します。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ミニポート ドライバーが、現在を報告する必要がありますも、ネットワーク アダプターで SR-IOV が有効な場合、アダプターのフィルタ リング設定を受信します。

    受信側のフィルター処理の機能の報告の詳細については、[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)を参照してください。

7.  呼び出しのコンテキストでは、次を行う必要があります、ミニポート ドライバーでは、静的な NIC スイッチの作成をサポートする場合[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)します。

    -   ドライバーは、NIC の標準化されたスイッチ キーワードの設定に基づいて、アダプターのハードウェアを構成します。 これらの設定に基づき、ドライバーは、NIC のスイッチのために必要なハードウェアおよびソフトウェア リソースを割り当てます。

    -   ミニポート ドライバー呼び出し[ **NdisMEnableVirtualization** ](https://msdn.microsoft.com/library/windows/hardware/hh451481) SR-IOV を有効にし、ネットワーク アダプターで VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で SR-IOV 対応の拡張機能を構成します。 この関数は、NDIS を返す場合\_状態\_成功した場合、SR-IOV が有効になっているし、VFs が、PCIe インターフェイスを介して公開されます。

    詳細については、[NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)を参照してください。

    **注**  ミニポート ドライバーでは、動的な NIC スイッチの作成をサポートする場合、スイッチを作成し、オブジェクト識別子 (OID) メソッド要求を処理する場合は、仮想化を有効[OID\_NIC\_スイッチ\_作成\_スイッチ](https://msdn.microsoft.com/library/windows/hardware/hh451815)します。 詳細については、[NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)を参照してください。

     

 

 





