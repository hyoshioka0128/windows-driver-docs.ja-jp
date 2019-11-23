---
title: 仮想ポートへの受信フィルターの移動
description: 仮想ポートへの受信フィルターの移動
ms.assetid: 6315FB18-3F57-43C2-B864-3759058092BB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28616bdb1c4519289af795b7dc780a24a888e68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844217"
---
# <a name="moving-a-receive-filter-to-a-virtual-port"></a>仮想ポートへの受信フィルターの移動


この後のドライバーは、オブジェクト識別子 (OID) セットの Oid 要求を発行します。 [\_受信フィルターを\_フィルター\_移動\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)を利用して、仮想ポート (vport) から NIC スイッチの別の vport に受信フィルターを移動します。 通常、次のいずれかの条件に該当する場合、仮想化スタックなどのそれ以降のドライバーは、この OID 要求を発行します。

-   仮想化スタックは、既定の VPort に受信フィルターを設定します。 このフィルターには、Hyper-v 子パーティションで公開されている仮想マシン (VM) ネットワークアダプターのメディアアクセスコントロール (MAC) アドレスと仮想 LAN (VLAN) のパラメーターが含まれています。 これにより、ソフトウェアベースの合成データパスを介して、VM ネットワークアダプターと基礎となるネットワークアダプターの間でパケットを転送できます。

    PCI Express (PCIe) 仮想機能 (VF) のリソースが割り当てられ、VF が子パーティションに接続されると、仮想化スタックによって、VF に既定以外の VPort が作成されます。 仮想化スタックは、VM ネットワークアダプターの受信フィルターを既定の VPort から、VF に接続されている既定以外の VPort に移動します。 これにより、ハードウェアベースの VF データパスを介して、VM ネットワークアダプターと基礎となるネットワークアダプターの間でパケットを転送できます。

    これらのデータパスの詳細については、「sr-iov[データパス](sr-iov-data-paths.md)」を参照してください。

-   VF は、ゲストオペレーティングシステムがまだ実行されている Hyper-v 子パーティションからデタッチされています。 この場合、前のドライバーは OID セット要求を発行して、VM ネットワークアダプターの受信フィルターを既定以外の VPort から、PF に接続されている既定の VPort に移動します。 この場合、パケットトラフィックは合成データパスに戻ります。

受信フィルターを1つの VPort から別の VPort に移動するには、その後のドライバーが oid セットの oid 要求を発行[\_、\_フィルター\_移動\_フィルターを受け取り](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)ます。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)\_\_パラメーター構造へのポインターが含まれています。\_

それ以降のドライバーは、 [\_フィルターを受け取る OID\_受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)する前に、フィルター要求\_フィルター要求\_移動\_\_の受信\_フィルター\_、次のように\_のパラメーター構造を[**移動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)する必要があります。

-   このドライバーは、 **Filterid**メンバーを、以前に割り当てられた受信フィルターの識別子の識別子に設定します。

    これまでのドライバーでは、以前の OID メソッドの Oid 要求からフィルター識別子を取得した  [\_受信\_フィルター\_設定さ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)れている**ことに注意**してください\_フィルター\_列挙\_フィルター\_列挙\_フィルター[列挙](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)します。

     

-   ドライバーは、 **Sourcequeueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定します。

-   ドライバーは、このフィルターが既に設定されている VPort の識別子に**SourceVPortId**メンバーを設定します。

-   このドライバーは、 **Destqueueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定します。

-   ドライバーは、このフィルターを移動する VPort の識別子に**DestVPortId**メンバーを設定します。

NDIS は、OID セット要求を PF ミニポートドライバーに転送する前に、 [ **\_受信\_フィルターを受け取る**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_move_filter_parameters)ことによって、ndis のメンバーを検証\_フィルター\_\_します。

PF ミニポートドライバーは、この OID セット要求を処理するときに、分割不可能な操作で受信フィルターを移動する必要があります。 ドライバーは、受信キューと VPort からフィルターを同時に削除し、別の受信キューと VPort に設定するように、ネットワークアダプターを構成できる必要があります。

 

 





