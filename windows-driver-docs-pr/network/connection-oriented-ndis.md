---
title: 接続指向 NDIS の概要
description: 接続指向 NDIS の概要
ms.assetid: c74f8e60-c041-48e9-8aa1-98a9cb9eb869
keywords:
- 接続指向の NDIS WDK
- CoNDIS WDK ネットワーク
- ネットワークドライバー WDK、CoNDIS
- NDIS WDK、CoNDIS
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 292d23d394ba300caa4d1f7a413b228fb973d23b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565769"
---
# <a name="connection-oriented-ndis"></a>接続指向 NDIS

このセクションでは、接続指向 NDIS (CoNDIS について説明します。 ほとんどの場合、6.0 以降のドライバー操作は、condis 5 から変更されていません。*x*バージョン。 Condis 5.x と condis 6.0 の相違点の詳細については、「 [condis 6.0 への Condis ドライバーの移植](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-a-condis-5-x-driver-to-condis-6-0)」を参照してください。

特に明記しない限り、CoNDIS ドライバーは、コネクションレス NDIS ドライバーと同じサービスを提供します。 CoNDIS ドライバーを記述する前に、コネクションレス NDIS ドライバーについて理解しておく必要があります。 コネクションレス NDIS ドライバーの詳細については、「 [Ndis ミニポートドライバーの記述](writing-ndis-miniport-drivers.md)」、「 [ndis プロトコルドライバー](writing-ndis-protocol-drivers.md)の記述」、および「 [ndis 中間ドライバーの記述](writing-ndis-intermediate-drivers.md)」を参照してください。

次のセクションでは、接続指向の NDIS について説明します。

[接続指向環境](connection-oriented-environment.md)

[AFs、VCs、Sap、およびパーティの使用](using-afs--vcs--saps--and-parties.md)

[サービスの品質](quality-of-service.md)

[MCM ドライバーと呼び出しマネージャー](mcm-drivers-vs--call-managers.md)

[接続指向のタイミング機能](connection-oriented-timing-features.md)

[CoNDIS 登録](condis-registration.md)

[接続指向の操作](connection-oriented-operations.md)

 

 





