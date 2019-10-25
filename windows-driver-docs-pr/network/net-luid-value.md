---
title: NET_LUID 値
description: NET_LUID 値
ms.assetid: 9b9c63c1-f8b4-4e26-afc1-a3e4910609e2
keywords:
- NDIS ネットワークインターフェイス WDK、NET_LUID
- ネットワークインターフェイス WDK、NET_LUID
- NET_LUID
- インデックス操作の WDK ネットワークインターフェイス
- ローカル一意識別子 WDK ネットワークインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad3539cdd0b4d584bf4e0a8c955161d06a085616
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829031"
---
# <a name="net_luid-value"></a>NET\_LUID 値





[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値は、NDIS ネットワークインターフェイスを識別する64ビット値です。 NET\_LUID データ型は、1つの64ビット値として、または NET\_LUID インデックスとインターフェイス型を含む構造体として、NET\_LUID 値へのアクセスを提供できる共用体です。

NET\_LUID 共用体の**Netluidindex**メンバーは、インターフェイスプロバイダーが[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)関数を呼び出すときに NDIS によって割り当てられる24ビットの NET\_luid インデックスです。 NDIS プロバイダーとインターフェイスプロバイダーは、このインデックスを使用して、同じインターフェイス型を持つ複数のインターフェイスを区別します。 したがって、このインデックスはローカルコンピューター内で一意です。

[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)共用体の**iftype**メンバーは、インターネット割り当て番号機関 (IANA) によって定義されたインターフェイス型を含む16ビット値です。 有効なインターフェイス型の一覧については、「 [NDIS インターフェイス型](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-interface-types)」を参照してください。

NDIS は、net\_LUID 値から*ifname*文字列を派生させるため、NET\_luid データ型は RFC 2863 の*ifname*オブジェクトに相当します。

NET\_LUID 値を作成するには、インターフェイスプロバイダーは[**NdisIfAllocateNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifallocatenetluidindex)関数を呼び出して、NET\_luid インデックスを割り当ててから、NDIS を呼び出し[ **\_\_net\_luid**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-net-luid)マクロを作成して net を構築し\_LUID 値。 NET\_LUID 値の作成の詳細については、「 [USING net\_Luid Indexes](using-a-net-luid-index.md)」を参照してください。

 

 





