---
title: アダプターからのバインド解除
description: アダプターからのバインド解除
ms.assetid: cea2ce45-df0c-4c75-a780-5810ea01b987
keywords:
- プロトコルのドライバー WDK ネットワーク、バインド解除
- NDIS ドライバー WDK のプロトコル バインドを解除
- アダプターの WDK ネットワークからバインド解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c64a82fc6da507ff8dd696256a03e60c7bd964f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579744"
---
# <a name="unbinding-from-an-adapter"></a>アダプターからのバインド解除





NDIS 呼び出しプロトコル ドライバーの[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)ドライバーが、基になるアダプターからバインド解除を要求する関数。 逆数として[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)、NDIS 呼び出し*ProtocolUnbindAdapterEx*をアダプターにバインドを閉じると、リソースを解放するドライバーバインディングに割り当てられます。

*ProtocolUnbindAdapterEx*、プロトコル ドライバーは呼び出し[ **NdisCloseAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561640)を基になるアダプターへのバインドを閉じます。 プロトコル ドライバー パス**NdisCloseAdapterEx**ハンドルを[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)で指定されているその*NdisBindingHandle*パラメーター。 このハンドルは、NDIS を閉じる必要があるバインディングを識別します。

プロトコル ドライバーからアダプターを閉じる必要があります、 *ProtocolBindAdapterEx*関数または*ProtocolUnbindAdapterEx*関数。

ドライバーを呼び出すことができる場合、プロトコル ドライバーには、バインディングを閉じる操作を開始する必要があります、 [ **NdisUnbindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff564630)します。 **NdisUnbindAdapter** NDIS 呼び出しで生成される作業項目をスケジュール*ProtocolUnbindAdapterEx*します。 この作業項目は、呼び出しの前に実行できる**NdisUnbindAdapter**を返します。 そのため、ドライバー作成者がバインド ハンドルが後に有効なことを想定する必要があります**NdisUnbindAdapter**を返します。

プロトコル ドライバーに返された NDIS 場合\_状態\_から PENDING *ProtocolUnbindAdapterEx*、呼び出す必要があります[ **NdisCompleteUnbindAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561708)バインド要求を完了する最終的な状態にします。

NDIS NDIS を返す場合\_状態\_から PENDING **NdisCloseAdapterEx**、NDIS 呼び出しプロトコル ドライバーの[ *ProtocolCloseAdapterCompleteEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570236)関数。

NDIS を呼び出すことができます*ProtocolUnbindAdapterEx*バインディングが一時停止状態にある場合。

すべてのバインドの解除操作が完了した後、バインドは、非連結状態です。

 

 





