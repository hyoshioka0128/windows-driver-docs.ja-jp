---
title: 仮想ポートでの受信フィルターのクリア
description: 仮想ポートでの受信フィルターのクリア
ms.assetid: 8431322B-2BF0-4F82-AAAE-0E0396BBC857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f17670dd0d30b5dcb41847c8b90cf0c4878ac2c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835177"
---
# <a name="clearing-a-receive-filter-on-a-virtual-port"></a>仮想ポートでの受信フィルターのクリア


NIC スイッチの仮想ポート (VPort) から受信フィルターをクリアするには、その後のドライバーが Oid のオブジェクト識別子 (OID) セット要求を発行[\_、\_フィルター\_クリア\_フィルターをクリア](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、 [**ndis\_RECEIVE\_FILTER\_CLEAR\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)構造体へのポインターが含まれています。

その後のドライバーが OID を発行する前に、フィルターの要求\_フィルター要求[\_クリア\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)によって、\_[**受信\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)を初期化し、\_パラメーター構造をクリアして設定する必要があり\_メンバーは次のようになります。

-   **Queueid**メンバーを NDIS\_既定\_受信\_キュー\_ID に設定する必要があります。

-   **Filterid**メンバーは、以前の\_oid から取得したドライバーがフィルターメソッド OID 要求[\_設定\_\_フィルターを受け取る](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)フィルター識別子の値に設定されている必要があります。 受信フィルターを設定する方法の詳細については、「[仮想ポートでの受信フィルターの設定](setting-a-receive-filter-on-a-virtual-port.md)」を参照してください。

このドライバーは、vport を解放する前に、VPort に設定されているすべてのフィルターをクリアする必要があります。 また、ネットワークアダプターへのバインドを閉じる前に、既定の VPort に設定されているすべてのフィルターをクリアする必要があります。

 

 





