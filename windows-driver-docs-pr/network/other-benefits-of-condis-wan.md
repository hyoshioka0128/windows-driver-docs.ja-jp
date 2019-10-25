---
title: CoNDIS WAN のその他の利点
description: CoNDIS WAN のその他の利点
ms.assetid: 5b937ae4-1486-4563-a863-5c02ba57c7df
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、特典
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 931ecf83e939311c043e6cf09a81529e61144fc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843755"
---
# <a name="other-benefits-of-condis-wan"></a>CoNDIS WAN のその他の利点





Conconwan モデルには、柔軟性とシンプルさに加えて、次のような利点があります。

-   Conmwan ミニポートドライバーは、マルチパケットの[送信操作と受信操作を](sending-and-receiving-data.md)サポートしています。

-   CoNDIS ミニポートドライバーが受信パケットを示している場合、バインドされたプロトコルはパケットの処理を遅らせることができます。 NDIS WAN ミニポートドライバーが受信パケットを示す場合、バインドされたプロトコルはデータを直ちにコピーする必要があります。

-   CoNDIS WAN は multipoint 呼び出しをサポートします。 マルチポイント呼び出しの詳細については、「[呼び出しを行う](making-a-call.md)」を参照してください。

-   CoNDIS WAN では、サービスの品質 (QoS) がサポートされています。 CoNDIS WAN ドライバーは、 [**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を使用します。 CoNDIS QoS の詳細については、「[クライアントが開始した要求の呼び出しパラメーターの変更](client-initiated-request-to-change-call-parameters.md)」を参照してください。

-   CoNDIS WAN のみが、WAN ドライバーに適用される将来の NDIS 拡張をサポートします。

 

 





