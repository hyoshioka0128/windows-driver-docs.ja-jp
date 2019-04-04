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
ms.openlocfilehash: e2ef2310844b37aef96cdcb26db00c1c795b4fe8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553744"
---
# <a name="binding-to-an-adapter"></a>アダプターへのバインド





NDIS 呼び出しプロトコル ドライバーの[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数バインディングを開くたびに、基になるアダプター ドライバーをバインドすることができるようになります。 NDIS 後*ProtocolBindAdapterEx*バインディングが Opening 状態に遷移します。 *開く*状態では、プロトコル ドライバーのバインディングのためのリソースの割り当てし、アダプターが表示されます。

NDIS に渡します*ProtocolBindAdapterEx* NDIS コンテキストへのポインターと同様に、バインド操作を[ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。 この構造体には、アダプターに関する情報にはなどが含まれます。

-   アダプターの名前。

-   レジストリのプロトコル サービスのエントリの下には、このバインディングに固有のパラメーターのレジストリの場所。

-   アダプターの物理デバイス オブジェクト。

アダプターを開くには、プロトコルのドライバーの呼び出し、 [ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)関数。 プロトコル ドライバーには、次の渡します**NdisOpenAdapterEx**:

-   NDIS にドライバーに返されたハンドルは、 *NdisProtocolHandle*のパラメーター、 **NdisRegisterProtocolDriver**関数。

-   このバインドのプロトコル ドライバーのコンテキスト。

-   型の構造体へのポインター [ **NDIS\_オープン\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566734)します。

[**NDIS\_開く\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566734)アダプターの名前などの情報が含まれていますを**NdisOpenAdapterEx**する必要がありますオープン、中規模の配列型をプロトコル ドライバーサポートと、必要に応じて、ドライバーは、このバインディングで受信できるフレームの種類の配列。

プロトコル ドライバーに返された NDIS 場合\_状態\_から PENDING *ProtocolBindAdapterEx*、呼び出す必要があります[ **NdisCompleteBindAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561702)バインド要求を完了する最終的な状態です。

NDIS NDIS を返す場合\_状態\_から PENDING **NdisOpenAdapterEx**、NDIS 呼び出しプロトコル ドライバーの[ *ProtocolOpenAdapterCompleteEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570265)オープン要求が完了した後、最終的な状態での関数。

ドライバーでは、アダプターにバインドが正常に開いたら、バインディングは一時停止状態です。

プロトコル ドライバーに呼び出し、 [ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)アダプターを閉じます。 ドライバーが呼び出せる**NdisCloseAdapterEx**から、 *ProtocolBindAdapterEx*関数または[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)関数。

場合、アダプターを起動して、バインド要求を完了する前に*ProtocolBindAdapterEx* 、エラーが発生し、バインドを閉じる必要があります、アダプターを呼び出すことができます**NdisCloseAdapterEx**します。 アダプターの終了についての詳細については、[アダプターからバインド解除](unbinding-from-an-adapter.md)を参照してください。

 

 





