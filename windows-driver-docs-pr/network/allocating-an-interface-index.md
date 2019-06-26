---
title: インターフェイス インデックスの割り当て
description: インターフェイス インデックスの割り当て
ms.assetid: f1315da2-16da-4320-9d0d-1270396af38b
keywords:
- NDIS ネットワーク インターフェイス、WDK インターフェイス インデックスの割り当て
- ネットワーク インターフェイス、WDK インターフェイス インデックスの割り当て
- インターフェイス インデックス WDK ネットワーク
- ネットワーク インターフェイスのインデックスの割り当てください。
- インデックス操作の WDK のネットワーク インターフェイス
- WDK ローカル一意識別子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e177131df795ddd6b2fcd77972f689674a9fbd87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382919"
---
# <a name="allocating-an-interface-index"></a>インターフェイス インデックスの割り当て





インターフェイスをプロバイダーが、呼び出すことによって、インターフェイスを正常に登録するかどうか、 [ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)関数、NDIS はそのインターフェイスのインターフェイス インデックスを割り当て、およびのインデックス値を返します場所を*pIfIndex*パラメーターを指定します。 インターフェイス インデックスは、ローカル コンピューター上で一意である 16 ビット値です。 NDIS は同じインターフェイスをプロバイダーの登録時に、同じインターフェイス インデックスを割り当てることは保証されません[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)コンピューターの再起動後の値。 インターフェイスのインデックス 0 の値 (NET\_IFINDEX\_未指定) は予約されている、および NDIS では任意のインターフェイスに割り当てられません。

 

 





