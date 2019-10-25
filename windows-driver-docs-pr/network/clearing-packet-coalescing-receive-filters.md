---
title: パケット結合受信フィルターのクリア
description: パケット結合受信フィルターのクリア
ms.assetid: 0924A494-AA4E-45FA-AFE6-65E0D105E0F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67eb0c8e475603329a99695b9d8ae5889ddd5f63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835173"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>パケット結合受信フィルターのクリア


パケット合体をサポートするミニポートドライバーで受信フィルターを解放または*クリア*するには、その後のドライバーが oid セットの oid 要求を発行[\_、\_フィルター\_クリア\_フィルターをクリア](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_FILTER\_CLEAR\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体へのポインターが含まれています。

プロトコルやフィルタードライバーなどの前のドライバーは、次の方法で[ **\_パラメーター構造をクリア\_、NDIS\_受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)を初期化します。

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

    **注**  NDIS 6.30 以降、パケット合体受信フィルターは、ネットワークアダプターの既定の受信キューでのみサポートされています。 この受信キューには、NDIS\_既定\_受信\_キュー\_ID の識別子が設定されています。

     

-   フィルタ**ID**メンバーは、ミニポートドライバーでクリアされるフィルターの0以外の識別子 (id) 値に設定する必要があります。 これまでのドライバーは、以前の OID メソッドの Oid 要求からフィルター ID を取得し、フィルターの\_または Oid を設定\_フィルターまたは Oid を受信\_フィルター\_[列挙型\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)フィルターを受け取るように設定して[\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)ます。

    **注**  パケット合体受信フィルターを設定した後のドライバーだけがクリアできます。

     

**  バインド**解除またはデタッチ操作を完了する前に、プロトコルまたはフィルタードライバーが、基になるミニポートドライバーで設定されているすべてのパケット合体受信フィルターをクリアする必要があります。

 

 

 





