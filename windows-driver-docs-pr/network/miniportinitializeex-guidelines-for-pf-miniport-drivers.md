---
title: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
description: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
ms.assetid: 338035E7-7677-49FE-A06D-CCFD813B0C10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61324d8f97a0a6827d2a98bb460afe7bcc422aff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380887"
---
# <a name="miniportinitializeex-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの MiniportInitializeEx ガイドライン


このトピックでは、書き込みのためのガイドラインを説明します、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)ミニポート ドライバーの PCI Express (PCIe) 物理機能 (PF) の関数。 PF は、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのコンポーネントです。

**注**  次のガイドラインは、PF ミニポート ドライバーにのみ適用されます。 PCIe 仮想機能 (VF) アダプターのミニポート ドライバーの初期化ガイドラインについては、次を参照してください。 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

 

PF のミニポート ドライバーが任意の NDIS ミニポート ドライバーと同じ手順に従うときにその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 次の手順の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

次の手順に加え、PF ミニポート ドライバーする必要があります追加の手順に従って NDIS ドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

1.  PF のミニポート ドライバー呼び出し、 [ **NdisGetHypervisorInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgethypervisorinfo)関数を HYPER-V 親パーティションで実行されていることを確認します。 この関数を返します、 [ **NDIS\_ハイパーバイザー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hypervisor_info)パーティションの種類を定義する構造体。 パーティションの種類として報告される場合**NdisHypervisorPartitionMsHvParent**、ミニポート ドライバーが、アダプターの PF にアタッチされている、HYPER-V 親パーティションで実行されています。

    **注**  として、パーティションの種類が報告された場合**NdisHypervisorPartitionMsHvChild**、ミニポート ドライバーが、アダプターの VF に関連付けられている HYPER-V 子パーティションで実行されています。 この場合は、PF ドライバーとしてミニポート ドライバーが初期化しないでください。 」の説明に従って、VF ドライバーとしてに初期化する必要があります、ドライバーの可能な場合は、 [VF のミニポート ドライバーの初期化](initializing-a-vf-miniport-driver.md)します。

     

2.  PF のミニポート ドライバーは、SR-IOV が標準化されているキーワード、SR-IOV が有効になっているかどうかを判断し、構成設定を取得するには、NIC のスイッチを読み取る必要があります。 これらのキーワードの詳細については、次を参照してください。 [SR-IOV の標準化された INF キーワード](standardized-inf-keywords-for-sr-iov.md)します。

    **注**  PF ミニポート ドライバーのエントリ ポイントが登録されているかどうか、 [ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数の場合、ドライバーが以前に取得からこれらの設定、NDIS が呼び出されたときに、レジストリ*MiniportSetOptions*します。

     

3.  ネットワーク アダプターでは、SR-IOV、仮想マシン キュー (VMQ) または RSS をサポートする場合、ミニポート ドライバーする必要があります、ネットワーク アダプターを有効にするには、どの機能を決定します。 これを確認する方法の詳細については、次を参照してください。[処理、SR-IOV、VMQ、および RSS の標準化された INF キーワード](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)します。

4.  RSS および VMQ のハードウェアの機能 (サポートされている) 場合、と共に、ミニポート ドライバーは、ハードウェア、SR-IOV 機能の完全なセットを報告する必要があります。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ネットワーク アダプターで SR-IOV が有効な場合、ミニポート ドライバーする必要があります、アダプターで現在 SR-IOV 設定がレポートも。

    レポートの SR-IOV 機能の詳細については、次を参照してください。 [SR-IOV 機能を決定する](determining-sr-iov-capabilities.md)します。

5.  ミニポート ドライバーには、そのハードウェア NIC スイッチ機能の完全なセットをレポートする必要があります。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ネットワーク アダプターで SR-IOV が有効な場合、ミニポート ドライバーする必要があります、アダプターで現在 NIC スイッチの設定がレポートも。

    スイッチ、NIC をレポート作成の詳細についてを参照してください[NIC スイッチ機能を決定する](determining-nic-switch-capabilities.md)します。

6.  ミニポート ドライバーがその全を報告する必要がありますのハードウェアのセットがフィルター処理機能を受信します。 レジストリで、SR-IOV が標準化されているキーワードの設定に関係なく、これらの機能を提供する必要があります。

    ミニポート ドライバーが、現在を報告する必要がありますも、ネットワーク アダプターで SR-IOV が有効な場合、アダプターのフィルタ リング設定を受信します。

    受信側のフィルター処理の機能の報告の詳細については、次を参照してください。[受信フィルタ リング機能を決定する](determining-receive-filtering-capabilities.md)します。

7.  呼び出しのコンテキストでは、次を行う必要があります、ミニポート ドライバーでは、静的な NIC スイッチの作成をサポートする場合[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)します。

    -   ドライバーは、NIC の標準化されたスイッチ キーワードの設定に基づいて、アダプターのハードウェアを構成します。 これらの設定に基づき、ドライバーは、NIC のスイッチのために必要なハードウェアおよびソフトウェア リソースを割り当てます。

    -   ミニポート ドライバー呼び出し[ **NdisMEnableVirtualization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismenablevirtualization) SR-IOV を有効にし、ネットワーク アダプターで VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で SR-IOV 対応の拡張機能を構成します。 この関数は、NDIS を返す場合\_状態\_成功した場合、SR-IOV が有効になっているし、VFs が、PCIe インターフェイスを介して公開されます。

    詳細については、次を参照してください。 [NIC スイッチの作成を静的](static-creation-of-a-nic-switch.md)します。

    **注**  ミニポート ドライバーでは、動的な NIC スイッチの作成をサポートする場合、スイッチを作成し、オブジェクト識別子 (OID) メソッド要求を処理する場合は、仮想化を有効[OID\_NIC\_スイッチ\_作成\_スイッチ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)します。 詳細については、次を参照してください。 [NIC スイッチの動的な作成](dynamic-creation-of-a-nic-switch.md)です。

     

 

 





