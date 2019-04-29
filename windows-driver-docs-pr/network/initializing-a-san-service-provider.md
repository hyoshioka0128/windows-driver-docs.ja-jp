---
title: SAN サービス プロバイダーの初期化
description: SAN サービス プロバイダーの初期化
ms.assetid: 73e923e9-c7bd-4d46-9d21-fc1392a79c65
keywords:
- SAN 使用率を初期化しています。 Windows Sockets 直接 WDK
- SAN 使用率の初期化
- SAN サービス プロバイダー、WDK の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb648da3f8c65306a287587fb73c1e57fdde264
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324997"
---
# <a name="initializing-a-san-service-provider"></a>SAN サービス プロバイダーの初期化





Windows Sockets スイッチでは、次の図の説明に従って、SAN サービス プロバイダーを初期化します。

![windows ソケットのスイッチがシステム エリア ネットワーク (san) のサービス プロバイダーを初期化する方法を示す図 ](images/apiflow1.png)

Windows 読み込み Windows Sockets では、アプリケーションのプロセスに DLL を切り替え、次の一連のイベントが発生します。

**SAN サービス プロバイダーを初期化するには**

1.  スイッチの検出、TCP/IP プロバイダーを読み込み、および」の説明に従って、これらのプロバイダーでは、すべてを検出するために、レジストリの SAN サービス プロバイダーの一覧を照会し[SAN サービス プロバイダーのインストール](installing-a-san-service-provider.md)します。 スイッチの呼び出しによって検出された各プロバイダーの[ **WSPStartupEx** ](https://msdn.microsoft.com/library/windows/hardware/ff566321)関数はそのプロバイダーの使用を開始します。

2.  **WSPStartupEx**呼び出し、スイッチはへのポインターを渡します、 [ **WSAPROTOCOL\_INFOW** ](https://msdn.microsoft.com/library/windows/hardware/ff565963) TCP/IP プロバイダーのプロトコルを含む構造体情報。 TCP/IP プロバイダーのプロトコルは、こと、初期化されている他の複数層サービス プロバイダーや、Windows ソケット インターフェイスではなく、スイッチで SAN サービス プロバイダーに示します。 スイッチは、Windows Sockets サービス プロバイダー、Microsoft Windows SDK ドキュメントのインターフェイス (SPI) のセクションで提案されている SAN サービス プロバイダーのトランスポートは、代わりに、TCP/IP プロバイダーのプロトコル情報を渡します。

    スイッチでそれが初期化されている SAN サービス プロバイダーが検出できる、ために、適切な一連のスイッチのエントリ ポイント関数を公開できます。 アプリケーションによって直接 SAN サービス プロバイダーが初期化される場合は、アプリケーションへのエントリ ポイント関数の別のセットが公開できます。 スイッチの下、SAN サービス プロバイダーが階層化されている場合、そのプロバイダーが拡張機能とこのセクションで説明した動作に従う必要があります。

3.  SAN サービス プロバイダーのプロキシ ドライバーは、」の説明に従って、その管理下にある各 NIC に割り当てられた IP アドレスの一覧を取得します。 [SAN NIC の通知を登録する](registering-for-san-nic-notifications.md)します。 SAN サービス プロバイダーでは、プライベート インターフェイスを使用して、そのプロキシ ドライバーからこの一覧を取得します。 スイッチの呼び出し、SAN サービス プロバイダーの[ **WSPSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff566319)ソケットを作成する関数。 スイッチでは、このソケットを使用して、SAN サービス プロバイダーのプロキシのドライバーの制御下での Nic に割り当てられた IP アドレスの完全な一覧を取得します。 スイッチが」の説明に従って、この一覧を取得[受信および変換の NIC アドレス](receiving-and-translating-nic-addresses.md)します。 この一覧およびその他の SAN サービス プロバイダーの一覧に基づいて、スイッチは、ローカルの IP サブネットを SAN サービス プロバイダーにマップするテーブルを作成します。

4.  Windows Sockets スイッチが使用するための Windows Sockets サービス プロバイダー インターフェイス (SPI) を拡張する SAN サービス プロバイダーのエントリ ポイント関数へのポインターを取得する必要がありますと San です。 Windows Sockets スイッチ、SAN サービス プロバイダーの呼び出しのこれらの関数の拡張を取得する[ **WSPIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff566296)関数を渡す、SIO\_取得\_拡張機能\_関数\_ポインター コマンド コード値を持つが次のいずれかを識別する GUID とは、関数を拡張します。

    これらの関数の詳細については、次を参照してください。 [Windows Sockets SPI Extensions for San](windows-sockets-spi-extensions-for-sans.md)します。

5.  スイッチを作成できます」の説明に従って、スレッドも非ブロッキング リスニング ソケットをサポートする接続要求、 [SAN 接続の設定](setting-up-a-san-connection.md)します。

 

 





