---
title: ネットワークインターフェイスの登録解除
description: ネットワークインターフェイスの登録解除
ms.assetid: 8d290a6a-008d-434b-bcbf-c4efade3d017
keywords:
- NDIS ネットワークインターフェイス WDK、登録解除
- ネットワークインターフェイス WDK、登録解除
- ネットワークインターフェイスの登録解除
- ネットワークインターフェイスの削除
- ネットワークインターフェイスの登録解除
- NdisIfDeregisterInterface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed4aad5b2de4aea32d523984a4f592f1e4466bcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838160"
---
# <a name="deregistering-a-network-interface"></a>ネットワークインターフェイスの登録解除





NDIS インターフェイスプロバイダーは、 [**NdisIfDeregisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterinterface)関数を呼び出して、指定されたインターフェイスをコンピューター上の既知のインターフェイスの一覧から削除する必要があることを示します。たとえば、インターフェイスがアンインストールされているためです。 インターフェイスの登録を解除するその他の理由は、アプリケーションによって異なります。 適切なリソース管理を促進するために、インターフェイスプロバイダーは、不要になったインターフェイスを常に登録解除する必要があります。

**NdisIfDeregisterInterface**は、指定されたインターフェイスに関連付けられているインターフェイスインデックスを解放します。 NDIS は、後で登録されているインターフェイスにインデックスを再割り当てできます。 ただし、対応する NET\_LUID 値に関連付けられている[**net\_luid**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)インデックスは解放されません。必要に応じて、インターフェイスプロバイダーは[**NdisIfFreeNetLuidIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiffreenetluidindex)を呼び出して、net\_LUID インデックスを解放できます。プロシージャ.

解除インターフェイスがアンインストールされ、モジュールがデタッチされたときにフィルターを適用する場合は、NDIS プロキシプロバイダーのインターフェイスを使用します **。  **

 

 

 





