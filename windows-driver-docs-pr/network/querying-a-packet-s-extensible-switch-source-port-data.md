---
title: パケットの拡張可能スイッチの発信元ポート データのクエリ
description: パケットの拡張可能スイッチの発信元ポート データのクエリ
ms.assetid: 082AEF58-3FCF-4ABE-90E1-1AC5DAF32B54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3938d6ada9671d0d06d0f4edf0653feb76648c44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844898"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポート データのクエリ


Hyper-v 拡張可能スイッチのソースポートは、NDIS\_スイッチの**SourcePortId**メンバーによって指定されます。 [ **\_転送\_詳細\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体です。 この構造体は、パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体の帯域外 (OOB) 転送コンテキストに含まれています。 このコンテキストの詳細については、「 [Hyper-v 拡張可能スイッチ転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)」を参照してください。

拡張可能なスイッチ拡張機能は、Net\_BUFFER\_LIST を使用して、 [**NDIS\_スイッチにアクセスし\_\_詳細\_net\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)構造体に転送し[ **\_\_転送\_詳細**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)マクロを切り替えます。 次の例では、ドライバーがパケットの NDIS\_スイッチから発信元ポートの識別子を取得して、 **\_詳細\_NET\_BUFFER\_LIST\_INFO 構造体\_転送**する方法を示します。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

 





