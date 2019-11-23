---
title: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
description: PF ミニポート ドライバーの MiniportInitializeEx ガイドライン
ms.assetid: 338035E7-7677-49FE-A06D-CCFD813B0C10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009ba15c94531db6a0169b367b56d40c2e862b0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844231"
---
# <a name="miniportinitializeex-guidelines-for-pf-miniport-drivers"></a>PF ミニポート ドライバーの MiniportInitializeEx ガイドライン


このトピックでは、PCI Express (PCIe) 物理機能 (PF) のミニポートドライバー用の[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を記述するためのガイドラインについて説明します。 PF は、シングルルート i/o 仮想化 (SR-IOV) をサポートするネットワークアダプターのコンポーネントです。

**注**  これらのガイドラインは、PF ミニポートドライバーにのみ適用されます。 アダプターの PCIe 仮想機能 (VF) のミニポートドライバーの初期化ガイドラインについては、「 [Vf ミニポートドライバーの初期化](initializing-a-vf-miniport-driver.md)」を参照してください。

 

PF ミニポートドライバーは、その[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)が機能するときに、NDIS ミニポートドライバーと同じ手順に従います。 これらの手順の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

これらの手順に加えて、NDIS ミニポートドライバーは、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すときに、次の追加の手順に従う必要があります。

1.  PF ミニポートドライバーは、 [**NdisGetHypervisorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgethypervisorinfo)関数を呼び出して、hyper-v の親パーティションで実行されていることを確認します。 この関数は、パーティションの種類を定義する[**NDIS\_ハイパーバイザー\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hypervisor_info)構造体を返します。 パーティションの種類が**NdisHypervisorPartitionMsHvParent**として報告された場合、ミニポートドライバーは、アダプターの PF に接続されている hyper-v の親パーティションで実行されています。

    **注**  パーティションの種類が**NdisHypervisorPartitionMsHvChild**として報告された場合、ミニポートドライバーは、アダプターの VF に接続されている hyper-v 子パーティションで実行されています。 この場合、ミニポートドライバーを PF ドライバーとして初期化することはできません。 可能な場合は、「 [Vf ミニポートドライバーの初期化](initializing-a-vf-miniport-driver.md)」で説明されているように、ドライバーを vf ドライバーとして初期化する必要があります。

     

2.  PF ミニポートドライバーは、sr-iov が有効になっているかどうかを判断し、NIC スイッチの構成設定を取得するために、sr-iov の標準化されたキーワードを読み取る必要があります。 これらのキーワードの詳細については、「sr-iov の標準化された[INF キーワード](standardized-inf-keywords-for-sr-iov.md)」を参照してください。

    **注**  PF ミニポートドライバーで[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数へのエントリポイントが登録されている場合、ドライバーは、NDIS が*MiniportSetOptions*を呼び出したときに、以前にこれらの設定をレジストリから取得した可能性があります。

     

3.  ネットワークアダプターが sr-iov、バーチャルマシンキュー (VMQ)、または RSS をサポートしている場合は、ネットワークアダプターで有効にする機能をミニポートドライバーで決定する必要があります。 これを確認する方法の詳細については、「sr-iov [、VMQ、RSS の標準化](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)された INF キーワードの処理」を参照してください。

4.  RSS および VMQ ハードウェア機能 (サポートされている場合) と共に、ミニポートドライバーは、ハードウェアの SR-IOV 機能の完全なセットを報告する必要があります。 これらの機能は、レジストリ内の SR-IOV の標準化されたキーワードの設定に関係なく、提供する必要があります。

    ネットワークアダプターで sr-iov が有効になっている場合、ミニポートドライバーは、アダプター上で有効になっている SR-IOV の設定も報告する必要があります。

    Sr-iov 機能のレポートの詳細については、「sr-iov[機能の決定](determining-sr-iov-capabilities.md)」を参照してください。

5.  ミニポートドライバーは、ハードウェアの NIC スイッチの完全な機能セットを報告する必要があります。 これらの機能は、レジストリ内の SR-IOV の標準化されたキーワードの設定に関係なく、提供する必要があります。

    ネットワークアダプターで sr-iov が有効になっている場合、ミニポートドライバーは、アダプター上で有効になっている NIC スイッチの設定も報告する必要があります。

    NIC スイッチ機能のレポートの詳細については、「 [Nic スイッチの機能の確認](determining-nic-switch-capabilities.md)」を参照してください。

6.  ミニポートドライバーは、ハードウェアの受信フィルター機能の完全なセットを報告する必要があります。 これらの機能は、レジストリ内の SR-IOV の標準化されたキーワードの設定に関係なく、提供する必要があります。

    ネットワークアダプターで sr-iov が有効になっている場合、ミニポートドライバーは、アダプター上で有効になっている受信フィルター設定も報告する必要があります。

    受信フィルター機能のレポートの詳細については、「[受信フィルター機能の決定](determining-receive-filtering-capabilities.md)」を参照してください。

7.  ミニポートドライバーで静的 NIC スイッチの作成がサポートされている場合は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の呼び出しのコンテキストで次の操作を行う必要があります。

    -   ドライバーは、NIC スイッチの標準化されたキーワードの設定に基づいてアダプターのハードウェアを構成します。 これらの設定に基づいて、ドライバーは NIC スイッチに必要なハードウェアおよびソフトウェアリソースを割り当てます。

    -   ミニポートドライバーは、 [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)を呼び出して sr-iov を有効にし、ネットワークアダプターの VFs の数を設定します。 この関数は、アダプターの PCI 構成領域で sr-iov 拡張機能を構成します。 この関数が NDIS\_STATUS\_SUCCESS を返した場合、SR-IOV が有効になり、VFs が PCIe インターフェイスを介して公開されます。

    詳細については、「 [NIC スイッチの静的作成](static-creation-of-a-nic-switch.md)」を参照してください。

    **注  :** ミニポートドライバーで動的な nic スイッチの作成がサポートされている場合は、スイッチを作成して仮想化を有効にします。これにより、\_nic\_のオブジェクト識別子 (oid) メソッドの要求を処理するときに、 [\_スイッチ\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)されます。 詳細については、「 [NIC スイッチの動的作成](dynamic-creation-of-a-nic-switch.md)」を参照してください。

     

 

 





