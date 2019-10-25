---
title: フィルター モジュール状態表示
description: フィルター モジュール状態表示
ms.assetid: b39c6cda-dac7-4538-8ea6-513a52601b1f
keywords:
- フィルターモジュール WDK ネットワーク、状態のインジケーター
- フィルタードライバーの WDK ネットワーク、状態のインジケーター
- NDIS フィルタードライバー WDK、状態のインジケーター
- WDK ネットワーク、フィルタードライバーに関するステータスを示す状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26fa7ad0a603c09d75e7e9b7bdf4d60f85ef5054
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838109"
---
# <a name="filter-module-status-indications"></a>フィルター モジュール状態表示





フィルタードライバーは、基になるドライバーがステータスを報告したときに NDIS が呼び出す[*Filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数を提供できます。 ドライバーのフィルターを使用して、状態のインジケーターを開始することもできます。

次の図は、フィルター処理された状態を示しています。

![フィルター処理された状態を示す図](images/statusfilter.png)

NDIS は、基になるドライバーがステータス表示関数 ([**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)または[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)) を呼び出すと、フィルタードライバーの[*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数を呼び出します。 ミニポートドライバーの状態を示す方法の詳細については、「[アダプターの状態](miniport-adapter-status-indications.md)の表示」を参照してください。

フィルタードライバーは、 [*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数内の**NdisFIndicateStatus**を呼び出して、フィルター処理された状態の表示を後続のドライバーに渡します。 フィルタードライバーは、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出さずに状態の表示を除外したり、 **NdisFIndicateStatus**を呼び出す前に示された状態を変更したりできます。

ステータスの兆候を生成するために、フィルタードライバーは、 [*Filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)を呼び出す前に[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出します。

この場合、フィルタードライバーは、 **Sourcehandle**メンバーを、 [*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数の*NdisFilterHandle*パラメーターに渡された NDIS ハンドルに設定する必要があります。 ステータス表示が OID 要求に関連付けられている場合、フィルタードライバーは**Destinationhandle**メンバーと**RequestId**メンバーを設定して、NDIS が特定のプロトコルバインドに状態を示すことができるようにすることができます。

フィルタードライバーが[**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)を呼び出すと、NDIS は次のドライバーの status 関数 ([**protocolstatusex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)または*filterstatus*) を呼び出します。

 

 





