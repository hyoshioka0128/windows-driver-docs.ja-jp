---
title: インターフェイス インデックスの割り当てください。
description: インターフェイス インデックスの割り当てください。
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
ms.openlocfilehash: d31446074b97bfda64a064564d7447249af36dd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531814"
---
# <a name="allocating-an-interface-index"></a>インターフェイス インデックスの割り当てください。





インターフェイスをプロバイダーが、呼び出すことによって、インターフェイスを正常に登録するかどうか、 [ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)関数、NDIS はそのインターフェイスのインターフェイス インデックスを割り当て、およびのインデックス値を返します場所を*pIfIndex*パラメーターを指定します。 インターフェイス インデックスは、ローカル コンピューター上で一意である 16 ビット値です。 NDIS は同じインターフェイスをプロバイダーの登録時に、同じインターフェイス インデックスを割り当てることは保証されません[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)コンピューターの再起動後の値。 インターフェイスのインデックス 0 の値 (NET\_IFINDEX\_未指定) は予約されている、および NDIS では任意のインターフェイスに割り当てられません。

 

 





