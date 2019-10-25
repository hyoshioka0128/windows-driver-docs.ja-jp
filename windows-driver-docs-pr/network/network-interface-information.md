---
title: ネットワーク インターフェイス情報
description: ネットワーク インターフェイス情報
ms.assetid: 4d8cd9c2-6f78-4c70-83bd-f36fffbf1c35
keywords:
- NDIS ネットワークインターフェイス WDK、情報
- ネットワークインターフェイス WDK、情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61390aa3b9ed90ce6910cc58cc25502e1e9dba63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827223"
---
# <a name="network-interface-information"></a>ネットワーク インターフェイス情報





インターフェイスプロバイダーは、次のデータ構造を使用して、登録されている各インターフェイスに関する情報を提供します。

-   [ **\_情報がある場合は NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_if_information)

-   [**NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)

インターフェイスを登録するために、プロバイダーは、 [**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数に情報構造を\_場合に、初期化された NET\_へのポインターを渡します。

NDIS インターフェイスプロバイダーは、 [OID\_GEN\_インターフェイス\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-interface-info)oid のクエリに応答して、 [**ndis\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)構造体を提供します。

また、NDIS は他の Oid でプロバイダーを照会することもできます。 NDIS プロバイダー Oid の詳細については、「 [Ndis ネットワークインターフェイスから oid へのマッピング](mapping-of-ndis-network-interfaces-to-ndis-oids.md)」を参照してください。 インターフェイスプロバイダーでの OID 要求の処理の詳細については、「 [NDIS インターフェイスプロバイダーでの Oid クエリおよび Set 要求の処理](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)」を参照してください。

 

 





