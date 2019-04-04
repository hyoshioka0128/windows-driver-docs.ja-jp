---
title: ネットワーク インターフェイスの情報
description: ネットワーク インターフェイスの情報
ms.assetid: 4d8cd9c2-6f78-4c70-83bd-f36fffbf1c35
keywords:
- NDIS ネットワーク インターフェイス、WDK について
- ネットワーク インターフェイス、WDK について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a3f4cd4e167badbb32513cd2604136fe912910
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552106"
---
# <a name="network-interface-information"></a>ネットワーク インターフェイスの情報





インターフェイス プロバイダーは、次のデータ構造を使用して、各登録済みのインターフェイスに関する情報を提供します。

-   [**NET\_場合\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff568743)

-   [**NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

インターフェイスを登録するには、プロバイダーの初期化の NET にポインターを渡します\_場合\_情報構造体、 [ **NdisIfRegisterInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff562715)関数。

NDIS インターフェイス プロバイダーを提供する[ **NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)のクエリに対する応答の構造、 [OID\_GEN\_インターフェイス\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569589)OID。

その他の Oid を持つプロバイダーをクエリ NDIS こともできます。 NDIS プロバイダー Oid の詳細については、[OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)を参照してください。 プロバイダーのインターフェイスで OID 要求の処理の詳細については、[OID クエリの処理および NDIS インターフェイス プロバイダーでの要求の設定](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)を参照してください。

 

 





