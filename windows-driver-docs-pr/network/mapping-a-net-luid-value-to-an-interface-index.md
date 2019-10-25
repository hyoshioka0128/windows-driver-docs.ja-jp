---
title: インターフェイス インデックスへの NET_LUID 値のマッピング
description: インターフェイス インデックスへの NET_LUID 値のマッピング
ms.assetid: a535d886-186e-4abe-9ca0-ebef262614b3
keywords:
- NDIS ネットワークインターフェイス WDK、NET_LUID
- ネットワークインターフェイス WDK、NET_LUID
- NET_LUID
- NET_LUID 値のマッピング
- インターフェイスインデックス WDK ネットワーク
- インデックス操作の WDK ネットワークインターフェイス
- ローカル一意識別子 WDK ネットワークインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b441ac12360acbbf19516bd2a586932f8023baa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844307"
---
# <a name="mapping-a-net_luid-value-to-an-interface-index"></a>NET\_LUID 値をインターフェイスインデックスにマップする





NDIS は、指定された[**NET\_LUID**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)値のインターフェイスインデックスを取得するサービスを提供します。逆も同様です。 NET\_LUID 値はインターフェイスの永続的な id であることに注意してください。特定の NET\_LUID 値に対応するインターフェイスインデックスは、コンピューターが再起動されない場合でも変更できます (たとえば、フィルターモジュールがアタッチされている場合など)。関連付けられているミニポートアダプターが無効になり、再度有効にされたために切断されました)。

NDIS には、次のマッピング関数が用意されています。

-   [**NdisIfGetInterfaceIndexFromNetLuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetinterfaceindexfromnetluid)

-   [**NdisIfGetNetLuidFromInterfaceIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifgetnetluidfrominterfaceindex)

これらの関数は、指定された NET\_LUID またはインターフェイスインデックスが登録されているインターフェイスの一覧に存在しない場合、NDIS\_STATUS\_INTERFACE\_\_を返します。

 

 





