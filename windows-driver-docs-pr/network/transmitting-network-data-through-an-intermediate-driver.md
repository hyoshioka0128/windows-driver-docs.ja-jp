---
title: 中間ドライバー経由のネットワーク データの転送
description: 中間ドライバー経由のネットワーク データの転送
ms.assetid: 90759322-810b-47fd-896c-465c96be4cdd
keywords:
- 中間ドライバー WDK ネットワーク、転送データ
- NDIS 中間ドライバー WDK、データの転送
- ネットワークデータの転送
- データ転送 WDK NDIS 中間
- データの転送 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3f5fe24a256ed82473cd2cb40f71f7e3fe88d25
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841774"
---
# <a name="transmitting-network-data-through-an-intermediate-driver"></a>中間ドライバー経由のネットワーク データの転送





「[中間ドライバーをミニポートドライバーとして登録](registering-an-intermediate-driver-as-a-miniport-driver.md)する」で説明されているように、中間ドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)に登録するときに[*miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数を提供する必要があります。 *Miniportsendnetbufferlists*関数は、ドライバーにコネクションレスエッジがある場合に[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)を呼び出すことによって、受信する[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体を転送できます。 *Miniportsendnetbufferlists*は、基になるミニポートドライバーの機能に関係なく、 **NdisSendNetBufferLists**によって受信される、NET\_BUFFER\_list 構造体の一覧を送信できます。

*Miniportsendnetbufferlists*は、 **NdisSendNetBufferLists**の呼び出し元によって決定された順序で配置された、NET\_BUFFER\_list 構造体の一覧を受け取ります。 ほとんどの場合、中間ドライバーは、この順序を維持する必要があります。これにより、受信した NET\_BUFFER\_LIST 構造体が、基になるミニポートドライバーに渡されます。 ネットワークデータ内のデータを基になるドライバーに渡す前に変更する中間ドライバーは、リストの順序を変更できます。

NDIS では、 **NdisSendNetBufferLists**にリンクリストとして渡されるように、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体ポインターの順序は常に保持されます。 また、基になるミニポートドライバーは、 *Miniportsendnetbufferlists*関数に渡されるリストが同じ順序でネットワークデータを送信する必要があることを前提としています。

 

 





