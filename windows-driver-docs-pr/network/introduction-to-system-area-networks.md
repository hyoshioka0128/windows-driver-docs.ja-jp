---
title: システム エリア ネットワークの概要
description: システム エリア ネットワークの概要
ms.assetid: 28d92bb5-8c3c-4f46-b908-63e3a3efff37
keywords:
- システム エリア ネットワークの詳細については、システム エリア ネットワーク WDK、
- システム エリア ネットワークについての SAN WDK
- WDK の San のハブ
- WDK の San のノード
- San 用の SAN NIC WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d4ae95050407d48ea488edbc1b447b80d76131
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329852"
---
# <a name="introduction-to-system-area-networks"></a>システム エリア ネットワークの概要





A*システム エリア ネットワーク (SAN)* 高パフォーマンス、接続指向のネットワークで、コンピューターのクラスターをリンクすることができます。 San の高帯域幅 (1 Gbps 以上) と低待機時間。 SAN は通常、8 つまたは複数のノードをサポートするためのハブで切り替えられます。 いくつかのキロメートルにいくつかのメーターから SAN 範囲でノード間のケーブルの長さ。

イーサネットや ATM などの既存のネットワーク テクノロジとは異なり、SAN はトランスポートの信頼性の高いサービスを提供していますつまり、送信された順序で破損していないデータを提供する SAN が保証されます。 SAN 内の接続エンドポイントは、TCP/IP プロトコル スタックを使用して、サブネット間でトラフィックをルーティングする必要がありますしない限り、データを転送する必要はありません。 SAN ローカル通信は、TCP/IP プロトコル スタックをバイパスする、ネイティブの SAN 転送を使用できます。

SAN ネットワーク インターフェイス コント ローラー (NIC)、SAN NIC のトランスポート ドライバーまたはその両方の組み合わせは、トランスポートのプライベート インターフェイスを公開します。 ただし、Windows Sockets を通じて TCP/IP を使用するほとんどのネットワーク アプリケーションが書き込まれるため、ことはできません、SAN を直接使用します。 [Windows Sockets 直接](windows-sockets-direct.md)コンポーネントの次の図に示すようにこれらのアプリケーションの変更を必要とせずに透過的に SAN を使用するメリットをできるようにします。 Windows ソケットの直接の一部を示します。

-   Microsoft Windows 2000 Datacenter Server

-   Microsoft Windows 2000 Advanced Server SP2

-   Microsoft Windows 2000 Server Appliance Kit SP2

-   Microsoft Windows Server 2003

次の図は、SAN をサポートするために必要なアーキテクチャを示します。 網掛けでは、SAN の使用を有効にする NIC の SAN ベンダーが提供するコンポーネントを表示します。

![システム エリア ネットワーク (san) をサポートするために必要なアーキテクチャを示す図](images/wsdpsan.png)

この図に示すように、コンポーネントの説明を次に示します。

<a href="" id="windows-sockets-application-------"></a>**Windows ソケット アプリケーション**   
アプリケーションのネットワーク サービス用の Windows ソケット インターフェイスです。

<a href="" id="windows-sockets-------"></a>**Windows ソケット**   
Windows ソケット インターフェイス (Ws2\_32.dll)。

<a href="" id="windows-sockets-spi-------"></a>**Windows Sockets SPI**   
Windows ソケット サービス プロバイダー インターフェイス (SPI)。

<a href="" id="windows-sockets-switch"></a>**Windows Sockets スイッチ**  
Windows ソケットは、標準の TCP/IP サービス プロバイダーを使用し、特定の SAN サービス プロバイダーの間で切り替わります。

<a href="" id="tcp-ip-service-provider"></a>**TCP/IP サービス プロバイダー**  
ユーザー モード DLL とを関連付けられているカーネル モード プロキシ ドライバー TCP/IP の基本 Windows Sockets サービスの標準的なプロバイダーを構成します。 プロキシ ドライバーでは、TDI インターフェイスを公開します。

<a href="" id="tcp-ip"></a>**TCP/IP**  
標準の TCP/IP プロトコル ドライバー。

<a href="" id="san-service-provider"></a>**SAN サービス プロバイダー**  
SAN サービス プロバイダーのユーザー モード DLL の部分。

<a href="" id="proxy-driver-for-a-san-service-provider"></a>**SAN サービス プロバイダーのプロキシ ドライバー**  
SAN サービス プロバイダーのカーネル モード プロキシ ドライバー。

<a href="" id="ndis-miniport-driver"></a>**NDIS ミニポート ドライバー**  
標準の TCP/IP プロトコル ドライバーを使用して SAN NIC への通信をサポートする NDIS ミニポート ドライバー。

<a href="" id="san-transport"></a>**SAN 転送**  
なトランスポートの信頼性の高いサービスを完全に実装できる、NIC、ソフトウェアでは、実装します。 または、ハードウェアとソフトウェアの組み合わせで実装された完全。

<a href="" id="san-nic"></a>**SAN の NIC**  
物理 SAN はネットワーク インターフェイス コント ローラー (NIC) です。

[]()  
特定の SAN のカーネル モード プロバイダー。 (将来の使用に備えて予約されています。)

 

 





