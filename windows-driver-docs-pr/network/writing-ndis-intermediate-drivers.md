---
title: NDIS 中間ドライバーの作成
description: NDIS 中間ドライバーの作成
ms.assetid: c37224b2-8d96-44c2-8b56-884089b9cfcd
keywords:
- 中間ドライバー WDK ネットワーク
- ネットワーク ドライバー WDK、中間ドライバー
- WDK NDIS 中間ドライバ
- NDIS 中間ドライバー WDK
- NDIS 中間ドライバー WDK、NDIS 6.0
- 中間ドライバー WDK ネットワー キング、NDIS 6.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778305aac1f12c04b2a1569e32533e7aba4fe4f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379776"
---
# <a name="writing-ndis-intermediate-drivers"></a>NDIS 中間ドライバーの作成





明記しない限り、NDIS 中間ドライバは、ミニポート ドライバーとプロトコル ドライバーとして同じサービスを提供します。 中間ドライバーのミニポート edge は、ミニポート ドライバー サービスを提供し、プロトコルのエッジはドライバー サービスのプロトコルを提供します。 (詳細については、次を参照してください[書き込み NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)と[書き込み NDIS プロトコル ドライバー](writing-ndis-protocol-drivers.md)。)。NDIS 6.0 と後で中間ドライバーの初期化は、従来の中間ドライバーの初期化と異なります。 また、NDIS 6.0 とそれ以降のドライバーは、結合されたミニポート中間ドライバーとして登録できます。

中間のドライバーの初期化の詳細については、以下のトピックです。

-   [中間のドライバーの初期化](initializing-an-intermediate-driver.md)
-   [ミニポート中間ドライバーの初期化](initializing-a-miniport-intermediate-driver.md)
-   [中間のドライバーをアンロード](unloading-an-intermediate-driver.md)
-   [仮想ミニポートの初期化](initializing-a-virtual-miniport.md)
-   [仮想ミニポートを停止します。](halting-a-virtual-miniport.md)

 

 





