---
title: 中間ドライバー バインド操作
description: 中間ドライバー バインド操作
ms.assetid: 129a744c-d4d4-4741-9812-e76087c585fc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b02a2c357de0a0a5e0a5df0129d46538429c235
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358615"
---
# <a name="intermediate-driver-binding-operations"></a>中間ドライバー バインド操作





NDIS を呼び出すミニポート アダプターが使用可能になるときに、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)そのミニポート アダプターにバインドできる任意の中間ドライバーの関数。

中間のドライバー提供プロトコル バインディング操作を記載する必要があります[をアダプターにバインド](binding-to-an-adapter.md)します。

バインディング時のアクションには、割り当てのアダプター固有のコンテキスト バインディングの領域を初期化し、仮想のミニポートの初期化、および呼び出しが含まれます[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)にバインドする、。アダプター。

中間のドライバーが個別に割り当てる必要はありません[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)バインディングごとにプールを構成します。 NET の割り当てに必要な中間ドライバー\_バッファー\_ドライバー デザインでは、独自の構造を割り当てることが必要な場合にのみプールの一覧の構造体。 それ以外の場合、ドライバーでは、他のドライバーから受信された構造に渡すことができますだけです。 このようなドライバーは、送信のための別のプールを割り当てるし、受信する必要があります。

割り当てし、ネットワークのデータを管理するための要件については、次を参照してください。[中間ドライバー ネットワーク データ管理](intermediate-driver-network-data-management.md)します。

 

 





