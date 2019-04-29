---
title: プロトコル ドライバーについて
description: プロトコル ドライバーについて
ms.assetid: a908f91e-7529-42b5-9a3d-82d2a519d969
keywords:
- プロトコル ドライバー WDK、コネクションレス ネットワーク下端
- NDIS プロトコル ドライバー WDK、コネクションレスの下端
- プロトコル ドライバー WDK ネットワーク、接続指向のクライアントおよびプロバイダー
- NDIS プロトコル ドライバー WDK、接続指向のクライアントとプロバイダー
- プロトコル ドライバー WDK ネットワー キング、Winsock サポート
- NDIS プロトコル ドライバー WDK、Winsock サポートします。
- Winsock カーネル WDK がネットワーク接続、Winsock のプロトコルのドライバー サポート
- ネットワーク ドライバー WDK、種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 855c11ba5759ced11eb1f37bde856286f35a19db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388757"
---
# <a name="learning-about-protocol-drivers"></a>プロトコル ドライバーについて





コネクションレス型、または接続指向の下端のいずれかのあるプロトコル ドライバーを記述することができます。 さらに、プロトコルには、ドライバーは、Winsock サポートを提供できます。 次の一覧では、WDK ドキュメントのセクションをお読みください、書き込みを行っているプロトコル ドライバーの種類に応じてについて説明します。

<a href="" id="protocol-drivers-that-have-a-connectionless-lower-edge"></a>**コネクションレスの下端にあるプロトコル ドライバー**  
プロトコル ドライバーの下端を記述する場合は、読み取り、コネクションレスのミニポート ドライバー インターフェイスを提供します。

-   [NDIS プロトコル ドライバー](ndis-protocol-drivers.md)

<a href="" id="protocol-drivers-that-are-connection-oriented-clients-or-that-are-connection-oriented-providers-of--------call-manager-services"></a>**クライアントの接続指向である、またはコール マネージャー サービスのプロバイダーの接続指向プロトコル ドライバー**  
接続指向のミニポート ドライバー インターフェイスを提供するには、接続指向のクライアントを作成する場合、または読み取り、接続指向のコール マネージャーを作成する場合。

-   [NDIS プロトコル ドライバー](ndis-protocol-drivers.md)

-   [接続指向の NDIS](connection-oriented-ndis.md)

<a href="" id="protocol-drivers-that-have-winsock-support"></a>**Winsock サポートされているプロトコル ドライバー**  
Winsock サポートを提供するプロトコルを記述する場合は、次の読み取り。

-   [NDIS プロトコル ドライバー](ndis-protocol-drivers.md)

-   [Windows ソケット トランスポートのヘルパー Dll](https://msdn.microsoft.com/library/windows/hardware/ff565691)

 

 





