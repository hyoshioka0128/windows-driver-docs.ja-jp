---
title: 中間ドライバーのプロトコルとしての登録
description: 中間ドライバーのプロトコルとしての登録
ms.assetid: 79707f6b-0e31-46a8-a763-fa2669ce9635
keywords:
- 中間ドライバーの登録
- ドライバー WDK 中級レベルのネットワーク、登録します。
- NDIS 中間ドライバ、WDK を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bc62c5a54a00b0f7642379bbc502776b05dd5b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374788"
---
# <a name="registering-an-intermediate-driver-as-a-protocol"></a>中間ドライバーのプロトコルとしての登録





中間のドライバーは、登録、 *ProtocolXxx* NDIS との関数のコンテキストでその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)関数を呼び出すことによって[ **NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)します。

プロトコルとして中間のドライバーの登録は、プロトコル ドライバーとして登録することとほぼ同じです。 詳細については、次を参照してください。[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)します。

接続指向の下端と中間のドライバーは、接続指向のクライアントとして登録する必要があります。 接続指向のクライアントでは、コール マネージャーまたは統合ミニポート コール マネージャー (MCM) の呼び出しセットアップと破棄のサービスを使用します。 接続指向のクライアントは、送信を使用してもと接続指向のミニポート ドライバーやデータを送受信する、MCM の機能を利用します。 詳細については、次を参照してください。 [Connection-Oriented 操作は、クライアントによって実行される](connection-oriented-operations-performed-by-clients.md)します。

中間のドライバーには、その他の必要があります*ProtocolXxx*実装に固有である関数。 省略可能な登録について*ProtocolXxx*関数を参照してください[省略可能なプロトコル ドライバー サービスを構成する](configuring-optional-protocol-driver-services.md)します。

 

 





