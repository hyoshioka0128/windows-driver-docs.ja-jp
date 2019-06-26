---
title: アダプターへのバインド
description: アダプターへのバインド
ms.assetid: 583b7c73-fbc7-4d25-95f7-973cede61ec8
keywords:
- プロトコル ドライバー WDK ネットワークは、アダプターへのバインド
- NDIS プロトコル ドライバー WDK、アダプターへのバインド
- バインディング操作の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e99891f580090206f9d745374a792cc5ef636e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386355"
---
# <a name="binding-to-an-adapter"></a>アダプターへのバインド





NDIS 呼び出しプロトコル ドライバーの[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数バインディングを開くたびに、基になるアダプター ドライバーをバインドすることができるようになります。 NDIS 後*ProtocolBindAdapterEx*バインディングが Opening 状態に遷移します。 *開く*状態では、プロトコル ドライバーのバインディングのためのリソースの割り当てし、アダプターが表示されます。

NDIS に渡します*ProtocolBindAdapterEx* NDIS コンテキストへのポインターと同様に、バインド操作を[ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)構造体。 この構造体には、アダプターに関する情報にはなどが含まれます。

-   アダプターの名前。

-   レジストリのプロトコル サービスのエントリの下には、このバインディングに固有のパラメーターのレジストリの場所。

-   アダプターの物理デバイス オブジェクト。

アダプターを開くには、プロトコルのドライバーの呼び出し、 [ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)関数。 プロトコル ドライバーには、次の渡します**NdisOpenAdapterEx**:

-   NDIS にドライバーに返されたハンドルは、 *NdisProtocolHandle*のパラメーター、 **NdisRegisterProtocolDriver**関数。

-   このバインドのプロトコル ドライバーのコンテキスト。

-   型の構造体へのポインター [ **NDIS\_オープン\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_open_parameters)します。

[**NDIS\_開く\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_open_parameters)アダプターの名前などの情報が含まれていますを**NdisOpenAdapterEx**する必要がありますオープン、中規模の配列型をプロトコル ドライバーサポートと、必要に応じて、ドライバーは、このバインディングで受信できるフレームの種類の配列。

プロトコル ドライバーに返された NDIS 場合\_状態\_から PENDING *ProtocolBindAdapterEx*、呼び出す必要があります[ **NdisCompleteBindAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletebindadapterex)バインド要求を完了する最終的な状態です。

NDIS NDIS を返す場合\_状態\_から PENDING **NdisOpenAdapterEx**、NDIS 呼び出しプロトコル ドライバーの[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)オープン要求が完了した後、最終的な状態での関数。

ドライバーでは、アダプターにバインドが正常に開いたら、バインディングは一時停止状態です。

プロトコル ドライバーに呼び出し、 [ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)アダプターを閉じます。 ドライバーが呼び出せる**NdisCloseAdapterEx**から、 *ProtocolBindAdapterEx*関数または[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数。

場合、アダプターを起動して、バインド要求を完了する前に*ProtocolBindAdapterEx* 、エラーが発生し、バインドを閉じる必要があります、アダプターを呼び出すことができます**NdisCloseAdapterEx**します。 アダプターの終了についての詳細については、次を参照してください。[アダプターからバインド解除](unbinding-from-an-adapter.md)します。

 

 





