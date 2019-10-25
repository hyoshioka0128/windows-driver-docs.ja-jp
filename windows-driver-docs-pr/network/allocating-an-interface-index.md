---
title: インターフェイス インデックスの割り当て
description: インターフェイス インデックスの割り当て
ms.assetid: f1315da2-16da-4320-9d0d-1270396af38b
keywords:
- NDIS ネットワークインターフェイス WDK、インターフェイスインデックスの割り当て
- ネットワークインターフェイス WDK、インターフェイスインデックスの割り当て
- インターフェイスインデックス WDK ネットワーク
- ネットワークインターフェイスインデックスを割り当てています
- インデックス操作の WDK ネットワークインターフェイス
- ローカル一意識別子 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e887742f5099b0e7192245a31b0af376ef0803a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835367"
---
# <a name="allocating-an-interface-index"></a>インターフェイス インデックスの割り当て





インターフェイスプロバイダーが[**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出すことによってインターフェイスを正常に登録すると、NDIS によってそのインターフェイスのインターフェイスインデックスが割り当てられ、 *pifindex*パラメーターの位置にあるインデックス値が返されます。か. インターフェイスインデックスは、ローカルコンピューター上で一意の16ビット値です。 NDIS は、コンピューターの再起動後にインターフェイスプロバイダーが同じ[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値を登録した場合に、同じインターフェイスインデックスが割り当てられることを保証しません。 インターフェイスインデックス値ゼロ (NET\_IFINDEX\_未指定) は予約されており、NDIS はインターフェイスに割り当てません。

 

 





