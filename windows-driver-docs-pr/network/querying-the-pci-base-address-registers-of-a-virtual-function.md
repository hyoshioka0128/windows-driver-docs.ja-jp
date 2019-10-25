---
title: 仮想関数の PCI ベース アドレス レジスターのクエリ
description: 仮想関数の PCI ベース アドレス レジスターのクエリ
ms.assetid: 99C2BF61-E87E-4C3B-BE7E-C16B5318EC1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee82180401a4dbcd3f01fb2e529eeb7440d7b0bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844869"
---
# <a name="querying-the-pci-base-address-registers-of-a-virtual-function"></a>仮想関数の PCI ベース アドレス レジスターのクエリ

**メモ**この方法は、Hyper-v の親パーティションの管理オペレーティングシステムで実行されるドライバーによってのみ使用できます。

Hyper-v 親パーティションの管理オペレーティングシステムで実行される PCI バスドライバーは、ネットワークアダプターの各 PCI ベースアドレスレジスタ (バー) のメモリまたは i/o アドレス空間の要件を照会します。 PCI バスドライバーは、バス上のアダプターを最初に検出したときに、このクエリを実行します。

Pci バスドライバーは、この PCI BAR クエリを使用して次のことを決定します。

-   PCI バーがネットワークアダプターによってサポートされているかどうか。

-   バーがサポートされている場合は、バーに必要なメモリまたは i/o アドレス空間の量を指定します。

PCI ドライバーは、次のように PCI バークエリを実行します。

1.  PCI ドライバーは、まずすべてのものをバーに書き込みます。

2.  次に、PCI ドライバーはバーを読み取って、バーに必要なメモリまたはアドレス空間を決定します。 値が0の場合は、そのバーがネットワークアダプターでサポートされていないことを示します。

仮想 PCI (VPCI) バスドライバーは、Hyper-v 子パーティションのゲストオペレーティングシステムで実行されます。 PCI Express (PCIe) 仮想関数 (VF) が子パーティションにアタッチされている場合、VPCI バスドライバーは VF (*vf ネットワークアダプター*) 用の仮想ネットワークアダプターを公開します。 これを行う前に、VPCI バスドライバーは、VF ネットワークアダプターに必要なメモリまたはアドレス空間を決定するために PCI バークエリを実行する必要があります。

PCI 構成領域へのアクセスは特権操作であるため、Hyper-v 親パーティションの管理オペレーティングシステムで実行されるコンポーネントによってのみ実行できます。 VPCI バスドライバーが PCI バーに対してクエリを実行すると、NDIS は[oid\_oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)のオブジェクト識別子 (oid) クエリ要求を発行し、\_バーを PF\_PF ミニポートドライバーに発行します。 この OID クエリ要求によって返される結果は、VF ネットワークアダプターで必要とされるメモリアドレス空間の量を決定できるように、VPCI バスドライバーに転送されます。

Oid **  oid**要求\_SRIOV\_BAR\_リソースは、NDIS によってのみ発行できます。 OID 要求は、プロトコルまたはフィルタードライバーなど、それ以降のドライバーによって発行されてはなりません。

 

OID\_SRIOV\_調査された\_バーのクエリ要求には、\_\_情報構造を調査した[**NDIS\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)が含まれています。 PF ミニポートドライバーがこの OID を処理する場合、ドライバーは、 **NDIS\_\_\_\_SRIOV**の**BaseRegisterValuesOffset**メンバーによって参照される配列内の PCI バーの値を返す必要があります。 PF ミニポートドライバーは、配列内のオフセットごとに、物理ネットワークアダプターの PCI 構成領域内の同じオフセットにあるバーの ULONG 値に配列要素を設定する必要があります。

ドライバーによって返される各棒値は、管理オペレーティングシステムで実行されている PCI ドライバーによって実行される PCI バークエリに続くものと同じ値である必要があります。 この情報を確認するために、PF ミニポートドライバーは[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)を呼び出すことができます。

PCI デバイスのベースアドレスレジスタの詳細については、 *Pci ローカルバスの仕様*を参照してください。

 

 





