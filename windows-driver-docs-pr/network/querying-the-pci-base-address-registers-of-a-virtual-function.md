---
title: 仮想関数の PCI ベース アドレス レジスターのクエリ
description: 仮想関数の PCI ベース アドレス レジスターのクエリ
ms.assetid: 99C2BF61-E87E-4C3B-BE7E-C16B5318EC1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774154db042ba94c4b4d2b42ea47b3786673811a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377046"
---
# <a name="querying-the-pci-base-address-registers-of-a-virtual-function"></a>仮想関数の PCI ベース アドレス レジスターのクエリ

**注**このメソッドは、HYPER-V 親パーティションの管理オペレーティング システムで実行されているドライバーの関連でのみ使用できます。

HYPER-V 親パーティションの管理オペレーティング システムで実行され、PCI バス ドライバーでは、メモリまたは I/O の各 PCI ベース アドレスを登録 (バー) のネットワーク アダプターのアドレス空間の要件を照会します。 PCI バス ドライバーは、最初にバス アダプターを検出した場合に、このクエリを実行します。

この PCI バー クエリによって、PCI バス ドライバーは、次で決定します。

-   かどうか、PCI バーは、ネットワーク アダプターによってサポートされます。

-   バーがサポートされている場合、どのくらいのメモリまたは I/O のアドレス空間がバーに必要です。

PCI ドライバは、次の方法でこの PCI バーのクエリを実行します。

1.  PCI ドライバは、まずバーへのすべてのものを書き込みます。

2.  PCI ドライバは、バーで必要とされる必要なメモリまたはアドレス領域を判断するのには、バーを読み取ります。 ゼロの値は、ネットワーク アダプターでは、バーがサポートされていないことを示します。

仮想の PCI (VPCI) バス ドライバーは、HYPER-V 子パーティションのゲスト オペレーティング システムで実行されます。 VPCI バス ドライバーが、VF のために、仮想ネットワーク アダプターを公開、PCI Express (PCIe) 仮想機能 (VF) が、子パーティションに関連付けられている場合 (*VF のネットワーク アダプター*)。 これは、前に、VPCI バス ドライバーは、必要なメモリまたは VF のネットワーク アダプターで必要とされるアドレス空間を決定する PCI バー クエリを実行する必要があります。

PCI の構成領域へのアクセスは、特権が必要であるために、HYPER-V 親パーティションの管理オペレーティング システムで実行されるコンポーネントによってのみ実行できます。 NDIS VPCI バス ドライバーでは、PCI バーを照会、発行オブジェクト識別子 (OID) のクエリ要求の[OID\_SRIOV\_PROBED\_バー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars) PF ミニポート ドライバーにします。 この OID クエリ要求によって返される結果は、メモリ アドレス領域の量は VF のネットワーク アダプターで必要になりますが確認できるように、VPCI バス ドライバーに転送されます。

**注**  OID の OID 要求\_SRIOV\_バー\_リソースは、NDIS でのみ発行できます。 プロトコルなどの上にあるドライバーまたはフィルター ドライバーによって、OID 要求は発行されませんする必要があります。

 

OID\_SRIOV\_PROBED\_バー クエリ要求に含まれる、 [ **NDIS\_SRIOV\_PROBED\_バー\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info)構造体。 ドライバーによって参照される配列内の PCI バーの値を返す必要があります、PF ミニポート ドライバーでは、この OID を処理する場合、 **BaseRegisterValuesOffset**のメンバー、 **NDIS\_SRIOV\_PROBED\_バー\_情報**構造体。 配列内の各オフセットの PF ミニポート ドライバーは、物理ネットワーク アダプターの PCI 構成領域内の同じオフセットにあるバーの ULONG 値に配列の要素を設定する必要があります。

同じ値は、管理オペレーティング システムで実行されている PCI ドライバによって実行される PCI バーのクエリを次に各棒、ドライバーによって返される値があります。 PF のミニポート ドライバーを呼び出すことができます[ **NdisMQueryProbedBars** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismqueryprobedbars)にこの情報を確認します。

PCI デバイスの詳細については、ベース アドレスのレジスタは、次を参照してください。、 *PCI ローカル バス仕様*します。

 

 





