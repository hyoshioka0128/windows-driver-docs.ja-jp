---
title: NET_LUID 値
description: NET_LUID 値
ms.assetid: 9b9c63c1-f8b4-4e26-afc1-a3e4910609e2
keywords:
- NDIS ネットワーク インターフェイス、WDK NET_LUID
- ネットワーク インターフェイス、WDK NET_LUID
- NET_LUID
- インデックス操作の WDK のネットワーク インターフェイス
- WDK ネットワーク インターフェイスのローカル一意識別子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d96f59e88cf84c6dd2da26796b0e353cc1a8b447
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550602"
---
# <a name="netluid-value"></a>NET\_LUID 値





A [ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)値は、NDIS のネットワーク インターフェイスを識別する 64 ビット値です。 NET\_LUID データ型は、NET にアクセスを提供する共用体\_LUID 値の 1 つの 64 ビット値、または、NET を格納する構造体として\_LUID インデックスとインターフェイスの種類します。

**NetLuidIndex** net メンバー\_LUID 共用体は、24 ビット NET\_インターフェイスをプロバイダーの呼び出し時に割り当て、NDIS LUID インデックス、 [ **NdisIfAllocateNetLuidIndex**](https://msdn.microsoft.com/library/windows/hardware/ff562695)関数。 NDIS とインターフェイスのプロバイダーは、同じインターフェイスの型を持つ複数のインターフェイスを区別する、このインデックスを使用します。 そのため、このインデックスは、ローカル コンピューター内で一意です。

**IfType**のメンバー、 [ **NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff568747)共用体は、Internet Assigned Numbers Authority の IANA で定義されているインターフェイスの種類を含む 16 ビット値。 有効なインターフェイスの種類の一覧は、次を参照してください。 [NDIS インターフェイス型](https://msdn.microsoft.com/library/windows/hardware/ff565767)します。

NET\_LUID データ型は等しく、*もし Name*オブジェクト RFC 2863、NDIS 派生するので、*もし Name* 、NET から文字列\_LUID 値。

ネットを作成する\_LUID 値では、インターフェイス プロバイダーを呼び出し、 [ **NdisIfAllocateNetLuidIndex** ](https://msdn.microsoft.com/library/windows/hardware/ff562695)関数を割り当てる、NET\_LUID インデックスに呼び出し、 [**NDIS\_ように\_NET\_LUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565890)ネットを構築するマクロ\_LUID 値。 NET の作成の詳細については\_LUID の値を参照してください[を使用して NET\_LUID インデックス](using-a-net-luid-index.md)します。

 

 





