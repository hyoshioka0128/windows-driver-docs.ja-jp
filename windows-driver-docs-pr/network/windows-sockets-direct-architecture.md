---
title: Windows ソケットは、アーキテクチャを直接します。
description: Windows ソケットは、アーキテクチャを直接します。
ms.assetid: 2f6ac4a7-76fe-45b4-8b5b-3a5f1d5c0553
keywords:
- Windows ソケットは、WDK、アーキテクチャを直接します。
- San の TCP/IP WDK
- NIC コンポーネント WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be57f40aeb1111a0e4ccb8f7254128a38b383cde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550615"
---
# <a name="windows-sockets-direct-architecture"></a>Windows ソケットは、アーキテクチャを直接します。





Windows Sockets ダイレクトは、SAN 転送のインターフェイスをアプリケーション プロセスに直接マップすることによって同じシステム エリア ネットワーク (SAN) 上の 2 つのネットワーク ノード間の高速で高性能な接続を提供します。 この SAN 接続により、ユーザー カーネルの境界を越えてコピーせずに直接入力と出力 (I/O) を実行するユーザー モード プロセスです。

SAN アーキテクチャの図[システム エリア ネットワークの概要](introduction-to-system-area-networks.md)がどのように Windows Sockets 直接提供 SAN 接続を示しています。 影付きの領域の図には、SAN の使用を有効にする SAN NIC ベンダーを指定する必要があるコンポーネントを表します。

次の段落には、図に表示されるコンポーネントについて説明します。

### <a name="supplied-components-for-san-network-interface-controllers"></a>SAN のネットワーク インターフェイス コント ローラーのコンポーネントに指定されました。

各 SAN ネットワーク インターフェイス コント ローラー (NIC) では、以下のソフトウェア コンポーネントを使用して、NDIS および Windows Sockets ダイレクトのサポートを提供します。

-   SAN の NIC の NDIS ミニポート ドライバーは、標準の TCP/IP プロトコル ドライバーを使用して、Windows ソケット アプリケーションと通信できるように、NDIS のサポートを提供します。 この NDIS ミニポート ドライバーでは、イーサネットや ATM などの標準的なメディアの種類をサポートします。

-   SAN サービス プロバイダーの DLL とその関連付けられているプロキシ ドライバーが Windows ソケットの直接のサポートを提供します。 これらの Windows Sockets 直接コンポーネントは、Windows ソケット アプリケーションに SAN の相互接続のネイティブのトランスポートのセマンティクスをエクスポートします。 このようなセマンティクス含めることができます、たとえば、アドレス ファミリとメッセージの方向。

SAN の NIC ベンダーには、NDIS ミニポート ドライバーと Windows Sockets ダイレクトのコンポーネントが用意されています。 トランスポートのサービスが NIC で完全に実装されていない場合、SAN の NIC ベンダーは SAN トランスポート ドライバーを提供も可能性があります。 NDIS ミニポート ドライバーまたは SAN NIC 仕入先の判断での個別のドライバーでの SAN サービス プロバイダーの DLL のプロキシ ドライバーや SAN トランスポート ドライバーが含まれています。

### <a name="windows-sockets-switch-components"></a>Windows ソケットのスイッチのコンポーネント

Windows Sockets スイッチは、Windows Sockets ダイレクトのオペレーティング システムが指定したコンポーネントです。 スイッチは、TCP/IP および SAN サービス プロバイダーの上に構築された Windows Sockets サービス プロバイダーです。 Windows オペレーティング システムでは、Windows ソケット インターフェイス、およびその他のサービス プロバイダー間の切り替えを挿入します。 わかりやすくするため、スイッチが個別のエンティティとしての図に表示されます。 ただし、スイッチと基本の TCP/IP サービス プロバイダー実際に同じ DLL に実装します。 スイッチは、次の操作を実行します。

-   SAN サービス プロバイダーと Windows ソケット アプリケーションへの 1 つのプロバイダーなどの標準的な TCP/IP プロバイダー外観のインストールされているコレクションを使用します。

-   選択、接続ごとに、アプリケーションのソケットをサービスに、ネイティブの SAN サービス プロバイダーまたは標準の TCP/IP プロバイダーを使用するかどうか。

-   ネイティブの SAN サービス プロバイダーを使用する場合は、TCP/IP セマンティックをエミュレートします。

スイッチの上端と下端のインターフェイスには、Windows Sockets サービス プロバイダー インターフェイス (SPI) に準拠しています。 スイッチの下のインターフェイスは、SAN の機能を活用するために Windows Sockets SPI の拡張機能を使用します。 これらの拡張機能が記載されて[Windows Sockets SPI Extensions for San](windows-sockets-spi-extensions-for-sans.md)で完全に文書化されていると、 [Windows Sockets の直接参照](https://msdn.microsoft.com/library/windows/hardware/ff565857)します。

スイッチは、アプリケーションのすべてのネットワークへのアクセスを管理します。 コンピューターには、複数の複数のベンダーから SAN Nic だけでなく 1 つまたは複数の LAN と WAN の Nic をイーサネット ネットワークをサポートしている LAN NIC などを含めることができます。 スイッチは、アプリケーションに透過的にこれらの Nic に関連付けられているすべてのネットワークへのアクセスを管理します。

### <a name="tcpip-functions"></a>TCP/IP 関数

NDIS を通じて公開される任意の NIC と同様、TCP/IP プロトコル ドライバーは各 SAN NIC に 1 つまたは複数の IP アドレスを割り当てます Windows ソケットの切り替えを」の説明に従って、SAN サービス プロバイダーがこれらの割り当てを判断[受信および変換の NIC アドレス](receiving-and-translating-nic-addresses.md)します。 スイッチは、SAN サービス プロバイダーが指定したソケット接続に使用するのに判断するために、この IP アドレス情報を使用します。 SAN サービス プロバイダーでは、この IP アドレス情報を使用して、ネイティブの SAN アドレスの IP アドレスに変換します。

スイッチは、SAN サービス プロバイダーをサポートしない機能を取得する基本 TCP/IP サービスの標準的なプロバイダーと密接に連携します。 TCP/IP サービスのプロバイダーは、複数のプロバイダーにわたる複数のプロバイダーとの同期で接続のリッスンをサポートします。

TCP/IP サービス プロバイダーもハンドルが標準の LAN および WAN 上のすべての通信が相互接続、生 IP ソケットの場合、すべての UDP ソケット、およびサブネット間の接続。

 

 





