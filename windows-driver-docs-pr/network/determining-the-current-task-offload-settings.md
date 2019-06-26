---
title: 現在のタスクのオフロード設定を決定します。
description: このセクションは、プロトコル ドライバーの現在のタスクのオフロード設定を確認する方法を説明します
ms.assetid: cd2f9b9f-f455-405d-8775-9a437e628476
keywords:
- タスクのオフロード WDK TCP/IP トランスポートでは、現在の設定
- 現在のタスクは、WDK TCP/IP offload の設定を読み込む
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bff5404a9a681c31675a417560fd5e94fe965aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381409"
---
# <a name="determining-the-current-task-offload-settings"></a>現在のタスク オフロード設定の判断


プロトコル ドライバーは、発行することによって、基になるミニポート アダプターの現在のタスク オフロードのカプセル化の設定を確認できます、 [OID\_オフロード\_カプセル化](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)OID クエリ要求。




OID 要求を発行の詳細については、次を参照してください。 [NDIS プロトコル ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-protocol-driver.md)します。

 

 





