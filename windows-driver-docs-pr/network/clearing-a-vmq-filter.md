---
title: VMQ フィルターのクリア
description: VMQ フィルターのクリア
ms.assetid: 34efeb28-dcd6-4a8b-89d2-6065830e03ab
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae482cc260d3e01aebc3b1c4addf900ef35f447
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838205"
---
# <a name="clearing-a-vmq-filter"></a>VMQ フィルターのクリア





受信キューのフィルターを解放するには、その後のドライバーが Oid を発行して、フィルター\_OID 要求を[クリア\_、\_フィルターを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_FILTER\_CLEAR\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体へのポインターが含まれています。

プロトコルドライバーは、以前の Oid からフィルター識別子を取得し、フィルター\_の OID 要求[\_設定して\_フィルターを受信\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)します。 フィルターの設定の詳細については、「 [VMQ フィルターの設定](setting-a-vmq-filter.md)」を参照してください。

プロトコルドライバーは、キューを解放する前に、キューに設定されているすべてのフィルターをクリアする必要があります。 また、プロトコルドライバーは、ネットワークアダプターへのバインドを閉じる前に、既定のキューに設定されているすべてのフィルターをクリアする必要があります。

\_フィルターを受け取る OID\_受信した場合は、ミニポートドライバーが既定以外のキューにあるパケットを示すことはできません。\_\_の OID 要求では、キューの最後のフィルターをクリアするか、Oid\_RECEIVE を完了しているかどうかを確認[\_フィルター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue) 、キューを解放するための無料\_キュー OID 要求です。

 

 





