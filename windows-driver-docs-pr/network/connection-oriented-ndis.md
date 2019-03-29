---
title: 接続指向 NDIS
description: 接続指向 NDIS
ms.assetid: c74f8e60-c041-48e9-8aa1-98a9cb9eb869
keywords:
- 接続指向の NDIS WDK
- ネットワークいる CoNDIS WDK
- ネットワーク ドライバー WDK、いる CoNDIS
- NDIS WDK、いる CoNDIS
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0a1292d411c851a0e5f66cc23ba1bfa2093d04e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570463"
---
# <a name="connection-oriented-ndis"></a>接続指向 NDIS





このセクションでは、接続指向の NDIS (いる CoNDIS) について説明します。 ほとんどのいる CoNDIS 6.0 とそれ以降のドライバー操作は、そのいる CoNDIS 5 から変更されていません。*x*バージョン。 いる CoNDIS 間の相違点の詳細については 5.x およびいる CoNDIS 6.0 を参照してください。[いる CoNDIS 6.0 への移植いる CoNDIS 5.x ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-a-condis-5-x-driver-to-condis-6-0)します。

明記しない限り、いる CoNDIS ドライバーはコネクションレスの NDIS ドライバーと同じサービスを提供します。 いる CoNDIS ドライバーを作成する前に、コネクションレスの NDIS ドライバー知識があります。 コネクションレスの NDIS ドライバーの詳細については、次を参照してください[書き込み NDIS ミニポート ドライバー](writing-ndis-miniport-drivers.md)、[書き込み NDIS プロトコル ドライバー](writing-ndis-protocol-drivers.md)、および[書き込み NDIS 中間ドライバ](writing-ndis-intermediate-drivers.md).

次のセクションでは、接続指向の NDIS について説明します。

[接続指向の環境](connection-oriented-environment.md)

[AFs、VCs、Sap、およびパーティの使用](using-afs--vcs--saps--and-parties.md)

[サービスの品質](quality-of-service.md)

[Vs の MCM ドライバー。コール マネージャー](mcm-drivers-vs--call-managers.md)

[タイミングの接続指向の機能](connection-oriented-timing-features.md)

[いる CoNDIS 登録](condis-registration.md)

[接続指向の操作](connection-oriented-operations.md)

 

 





