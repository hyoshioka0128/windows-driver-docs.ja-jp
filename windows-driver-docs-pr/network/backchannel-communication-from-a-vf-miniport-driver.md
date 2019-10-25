---
title: VF ミニポート ドライバーからのバックチャネル通信
description: VF ミニポート ドライバーからのバックチャネル通信
ms.assetid: B7208199-1308-4EF1-A03B-237A283563C4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c43e84c96d4c0052eae26ee05b6e88986c97a21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835282"
---
# <a name="backchannel-communication-from-a-vf-miniport-driver"></a>VF ミニポート ドライバーからのバックチャネル通信


PCI Express (PCIe) 仮想機能 (VF) のミニポートドライバーは、PCIe 物理機能 (PF) のミニポートドライバーと通信して、VF 構成ブロックのデータの読み取りまたは書き込みを行います。

VF 構成ブロックは、PF および VF ミニポートドライバー間のバックチャネル通信に使用されます。 独立系ハードウェアベンダー (IHV) は、デバイスの1つまたは複数の VF 構成ブロックを定義できます。 各 VF 構成ブロックには、IHV によって定義された形式、長さ、およびブロック ID があります。 たとえば、IHV は、VF ミニポートドライバーのメディアアクセスコントロール (MAC) アドレスに使用できる VF 構成ブロックを定義できます。 別の VF 構成ブロックは、現在の VF と仮想ポート (VPort) の構成に使用できます。

  **注**各 VF 構成ブロックのデータは、PF および vf ミニポートドライバーによってのみ使用されます。 このデータの形式と内容は、Windows オペレーティングシステムのコンポーネントに対して非透過的です。

 

各 VF 構成ブロックには、IHV によって一意の識別子が割り当てられます。 これにより、VF ミニポートドライバーは、特定の VF 構成ブロックに関する情報を照会または設定できます。

VF ミニポートドライバーは、次の関数を使用して、指定された VF 構成ブロックで読み取りまたは書き込み操作を開始します。

-   [**NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)。指定された VF 構成ブロックからデータを読み取ります。 VF ミニポートドライバーは、この関数を呼び出すときに、読み取るデータのブロック識別子と長さを指定します。 また、ドライバーは、要求されたデータを格納するバッファーへのポインターも渡します。

-   [**NdisMWriteConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)。指定した VF 構成ブロックにデータを書き込みます。 VF ミニポートドライバーは、この関数を呼び出すときに、書き込まれるデータのブロック識別子と長さを指定します。 また、ドライバーは、データの書き込み元のバッファーへのポインターも渡します。

PF ミニポートドライバーは、次の方法で、指定された VF 構成ブロックへのアクセスを管理します。

-   VF ミニポートドライバーが[**NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)を呼び出すと、NDIS は\_oid のオブジェクト識別子 (oid) メソッド要求を SRIOV に発行し、 [\_VF\_CONFIG\_ブロック](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-block)を PF ミニポートドライバーに読み取り\_ます。 この OID 要求には、関数呼び出しで VF ミニポートドライバーによって渡されたパラメーターデータが含まれています。

    PF ミニポートドライバーは、読み取り操作を実行し、ドライバーが OID 要求を完了すると、要求されたデータを返します。 OID 要求が完了すると、NDIS は[**NdisMReadConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)の呼び出しからを返します。

-   VF ミニポートドライバーが[**NdisMWriteConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)を呼び出すと、NDIS は OID\_SRIOV の oid メソッド要求を発行し[\_\_VF\_CONFIG\_ブロック](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-block)を PF ミニポートドライバーに書き込みます。 この OID 要求には、関数呼び出しで VF ミニポートドライバーによって渡されたパラメーターデータが含まれています。

    PF ミニポートドライバーは書き込み操作を実行し、OID 要求を完了します。 OID 要求が完了すると、NDIS は[**NdisMWriteConfigBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)の呼び出しからを返します。

次の図は、SR-IOV バックチャネルインターフェイスを介した VF 構成ブロックの読み取りと書き込みに関係するプロセスを示しています。

![画像は、vf ミニポートドライバー、ndis、および pf ミニポートドライバー間で移動するさまざまな構成ブロックを示しています。](images/sriov-vf-backchannel.png)

 

 





