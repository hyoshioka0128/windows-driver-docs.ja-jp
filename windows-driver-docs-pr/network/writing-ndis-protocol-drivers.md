---
title: NDIS プロトコル ドライバーの作成
description: NDIS プロトコル ドライバーの作成
ms.assetid: 30d27b9b-e6b9-4548-ab83-f240e60d5393
keywords:
- プロトコル ドライバーについて、ドライバー WDK のプロトコルのネットワーク、
- NDIS プロトコル ドライバーに関するプロトコル ドライバー WDK、NDIS
- NDIS プロトコル ドライバー WDK、書き込み
- プロトコル ドライバー WDK ネットワーク、書き込み
- NDIS プロトコル ドライバー WDK ネットワークの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0324bc86943bd0b00f3533107a26954b6dde5fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582042"
---
# <a name="writing-ndis-protocol-drivers"></a>NDIS プロトコル ドライバーの作成





このドキュメントでは、NDIS 6.0 以降のドライバー操作プロトコルの概要を示します。 NDIS プロトコル ドライバー提供*ProtocolXxx*関数呼び出し、NDIS、操作を開始します。 NDIS 提供**Ndis * Xxx*** プロトコルのドライバー呼び出し操作を実行する関数。

次のトピックでは、バインドの状態と、操作の間のリレーションシップを記述し、いくつかのプロトコル ドライバー操作の概要が含まれます。

-   [プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)
-   [プロトコル バインドの状態と操作](protocol-binding-states-and-operations.md)
-   [アダプターへのバインド](binding-to-an-adapter.md)
-   [アダプターからバインド解除](unbinding-from-an-adapter.md)
-   [開始して、バインディングを一時停止](starting-and-pausing-a-binding.md)
-   [省略可能なプロトコル ドライバー サービスを構成します。](configuring-optional-protocol-driver-services.md)
-   [プロトコル ドライバーの送信し、受信操作](protocol-driver-send-and-receive-operations.md)
-   [プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)
-   [プロトコル ドライバーに状態インジケーターの処理](handling-status-indications-in-a-protocol-driver.md)
-   [プロトコル ドライバーでの PnP イベント通知の処理](handling-pnp-event-notifications-in-a-protocol-driver.md)

 

 





