---
title: インターフェイス インデックスへの NET_LUID 値のマッピング
description: インターフェイス インデックスへの NET_LUID 値のマッピング
ms.assetid: a535d886-186e-4abe-9ca0-ebef262614b3
keywords:
- NDIS ネットワーク インターフェイス、WDK NET_LUID
- ネットワーク インターフェイス、WDK NET_LUID
- NET_LUID
- NET_LUID 値のマッピング
- インターフェイス インデックス WDK ネットワーク
- インデックス操作の WDK のネットワーク インターフェイス
- WDK ネットワーク インターフェイスのローカル一意識別子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b312b9f90eb9c01815d9f91db7be5fc365202b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572405"
---
# <a name="mapping-a-netluid-value-to-an-interface-index"></a>マッピング、NET\_インターフェイス インデックスに LUID 値





NDIS のインターフェイス インデックスを取得するサービスを提供する、指定された[ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)値、またはその逆です。 なお、NET\_LUID 値は、インターフェイス、および特定のネットワークに対応するインターフェイスのインデックスの id を永続的な\_場合でも、コンピューターは再起動しません (たとえば、フィルター モジュール LUID の値を変更することができますアタッチ、デタッチ、関連付けられているミニポート アダプターが無効になり、再び有効にするため)。

NDIS は、次のマッピング機能を提供します。

-   [**NdisIfGetInterfaceIndexFromNetLuid**](https://msdn.microsoft.com/library/windows/hardware/ff562707)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](https://msdn.microsoft.com/library/windows/hardware/ff562711)

これらの関数は、NDIS を返す\_状態\_インターフェイス\_いない\_見つかった場合、特定の NET\_LUID またはインターフェイス インデックスが登録されているインターフェイスのリストに存在しません。

 

 





