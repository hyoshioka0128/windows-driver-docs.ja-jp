---
title: タスク オフロード サービスの有効化と無効化
description: プロトコル ドライバーでは、有効にしたり、OID_OFFLOAD_ENCAPSULATION OID のセット要求を発行して基になるミニポート アダプターのタスクのオフロード サービスを無効にすることができます。
ms.assetid: cc803af4-d4ed-4b51-9e0e-77443e0eb023
keywords:
- タスクのオフロード WDK TCP/IP トランスポートは、サービスを有効にします。
- タスクのオフロード WDK TCP/IP トランスポートは、サービスを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 294d006b596b21477c817c60b6c957a7dd6ee8c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573411"
---
# <a name="enabling-and-disabling-task-offload-services"></a>タスク オフロード サービスの有効化と無効化


プロトコル ドライバーが有効にするまたは発行することによって基になるミニポート アダプターのタスクのオフロード サービスを無効にする、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)OID が要求を設定します。 この OID 要求は、必要なカプセル化の種類を設定し、すべての利用可能なタスク オフロード サービスをアクティブ化するミニポート ドライバーに指示します。




発行する前に、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)OID 要求の設定、プロトコルのドライバーが基になるミニポート アダプターが必要なカプセル化の種類をサポートしていることを確認してください。 これには 2 つの方法があります。

-   チェック、 [ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)で受信したプロトコル ドライバー構造の[ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。
-   問題を[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)クエリ要求。

ミニポート ドライバーでは、要求されたカプセル化の種類をサポートしているタスク オフロードの種類をサポートする場合、ミニポート ドライバーが NDIS を返す必要があります\_状態\_への応答の成功、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)セットの要求。 ミニポート ドライバーで NDIS を返す必要がありますそれ以外の場合、\_状態\_無効な\_パラメーター。

 

 





