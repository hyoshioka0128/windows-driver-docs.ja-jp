---
title: NDIS 中間ドライバーの記述の概要
description: NDIS 中間ドライバーの記述の概要
ms.assetid: c37224b2-8d96-44c2-8b56-884089b9cfcd
keywords:
- 中間ドライバー WDK ネットワーク
- ネットワークドライバー WDK、中間ドライバー
- NDIS WDK、中間ドライバー
- NDIS 中間ドライバー WDK
- NDIS 中間ドライバー WDK、NDIS 6.0
- 中間ドライバー WDK ネットワーク、NDIS 6.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 927f6f1076f0a70f9b419d976cc8fdf90a063740
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565707"
---
# <a name="getting-started-writing-ndis-intermediate-drivers"></a>NDIS 中間ドライバーの記述の概要

特に明記されていない限り、NDIS 中間ドライバーはミニポートドライバーおよびプロトコルドライバーと同じサービスを提供します。 中間ドライバーのミニポートエッジは、ミニポートドライバーサービスを提供し、プロトコルエッジはプロトコルドライバーサービスを提供します。 (詳細については、「 [Ndis ミニポートドライバーの記述](writing-ndis-miniport-drivers.md)」および「 [ndis プロトコルドライバーの記述](writing-ndis-protocol-drivers.md)」を参照してください)。NDIS 6.0 以降の中間ドライバーの初期化は、レガシ中間ドライバーの初期化とは異なります。 また、NDIS 6.0 以降のドライバーは、ミニポート中間ドライバーとして登録できます。

次のトピックでは、中間ドライバーの初期化の詳細について説明します。

-   [中間ドライバーの初期化](initializing-an-intermediate-driver.md)
-   [ミニポート中間ドライバーの初期化](initializing-a-miniport-intermediate-driver.md)
-   [中間ドライバーのアンロード](unloading-an-intermediate-driver.md)
-   [仮想ミニポートの初期化](initializing-a-virtual-miniport.md)
-   [仮想ミニポートの停止](halting-a-virtual-miniport.md)

 

 





