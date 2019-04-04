---
title: パケットの拡張可能スイッチの発信元ポートのデータを照会します。
description: パケットの拡張可能スイッチの発信元ポートのデータを照会します。
ms.assetid: 082AEF58-3FCF-4ABE-90E1-1AC5DAF32B54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a1c30ff1d5950ffe5259baefae02114de154032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550106"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>パケットの拡張可能スイッチの発信元ポートのデータを照会します。


HYPER-V 拡張可能スイッチの発信元ポートが指定された、 **SourcePortId**内のメンバー、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体。 この構造体の帯域外 (OOB) コンテキストのパケットの転送に含まれている[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 このコンテキストの詳細については、[Hyper-v 拡張可能スイッチの転送コンテキスト](hyper-v-extensible-switch-forwarding-context.md)を参照してください。

拡張可能スイッチの拡張機能にアクセス、 [ **NDIS\_切り替える\_転送\_詳細\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh598211)構造体を使用して、 [ **NET\_バッファー\_一覧\_スイッチ\_転送\_詳細**](https://msdn.microsoft.com/library/windows/hardware/hh598259)マクロ。 次の例は、ドライバーがからパケットの送信元ポートの識別子を取得する方法を示しています**NDIS\_スイッチ\_転送\_詳細\_NET\_バッファー\_ 。リスト\_情報**構造体。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

 





