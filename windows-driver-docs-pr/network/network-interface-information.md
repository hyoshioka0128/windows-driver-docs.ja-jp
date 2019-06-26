---
title: ネットワーク インターフェイス情報
description: ネットワーク インターフェイス情報
ms.assetid: 4d8cd9c2-6f78-4c70-83bd-f36fffbf1c35
keywords:
- NDIS ネットワーク インターフェイス、WDK について
- ネットワーク インターフェイス、WDK について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a751ba458056303ff005d911f0b3617ef3093e3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386319"
---
# <a name="network-interface-information"></a>ネットワーク インターフェイス情報





インターフェイス プロバイダーは、次のデータ構造を使用して、各登録済みのインターフェイスに関する情報を提供します。

-   [**NET\_場合\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_if_information)

-   [**NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)

インターフェイスを登録するには、プロバイダーの初期化の NET にポインターを渡します\_場合\_情報構造体、 [ **NdisIfRegisterInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)関数。

NDIS インターフェイス プロバイダーを提供する[ **NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)のクエリに対する応答の構造、 [OID\_GEN\_インターフェイス\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)OID。

その他の Oid を持つプロバイダーをクエリ NDIS こともできます。 NDIS プロバイダー Oid の詳細については、次を参照してください。 [OID マッピングをネットワーク インターフェイスの NDIS](mapping-of-ndis-network-interfaces-to-ndis-oids.md)します。 プロバイダーのインターフェイスで OID 要求の処理の詳細については、次を参照してください。 [OID クエリの処理および NDIS インターフェイス プロバイダーでの要求の設定](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)します。

 

 





