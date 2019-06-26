---
title: パケットの拡張可能スイッチの発信元ポート データのクエリ
description: パケットの拡張可能スイッチの発信元ポート データのクエリ
ms.assetid: 082AEF58-3FCF-4ABE-90E1-1AC5DAF32B54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8749e6ac25f0f6ca48da5bbd9711dbd5ac79d6e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385435"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポート データのクエリ


HYPER-V 拡張可能スイッチの発信元ポートが指定された、 **SourcePortId**内のメンバー、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体。 この構造体の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 このコンテキストの詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)します。

拡張可能スイッチの拡張機能にアクセス、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体を使用して、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロ。 次の例は、ドライバーがからパケットの送信元ポートの識別子を取得する方法を示しています**NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_ 。リスト\_情報**構造体。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

 





