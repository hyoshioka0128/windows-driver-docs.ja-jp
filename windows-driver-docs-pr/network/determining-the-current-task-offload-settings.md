---
title: 現在のタスクのオフロード設定を決定します。
description: このセクションは、プロトコル ドライバーの現在のタスクのオフロード設定を確認する方法を説明します
ms.assetid: cd2f9b9f-f455-405d-8775-9a437e628476
keywords:
- タスクのオフロード WDK TCP/IP トランスポートでは、現在の設定
- 現在のタスクは、WDK TCP/IP offload の設定を読み込む
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3edc57ecb3bdd3520be9908f3a65c76a5579cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364205"
---
# <a name="determining-the-current-task-offload-settings"></a>現在のタスク オフロード設定の判断


プロトコル ドライバーは、発行することによって、基になるミニポート アダプターの現在のタスク オフロードのカプセル化の設定を確認できます、 [OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)OID クエリ要求。




OID 要求を発行の詳細については、次を参照してください。 [NDIS プロトコル ドライバーから OID の要求を生成する](generating-oid-requests-from-an-ndis-protocol-driver.md)します。

 

 





