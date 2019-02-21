---
title: SAN サービス プロバイダーのインストール
description: SAN サービス プロバイダーのインストール
ms.assetid: 3a7fcacf-ef26-4a41-a991-230daf67accf
keywords:
- コンポーネントをインストールする Windows Sockets 直接 WDK
- SAN サービス プロバイダー、WDK をインストールします。
- SAN サービス プロバイダーに登録します。
- 登録の SAN サービス プロバイダー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62a857e152a43f844dcf79ef7310d3f7ad69b220
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558690"
---
# <a name="installing-a-san-service-provider"></a>SAN サービス プロバイダーのインストール





通常、SAN サービス プロバイダーは、Windows Sockets スイッチとのインターフェイスは、基本 Windows Sockets サービス プロバイダーとしてインストールされます。 SAN サービス プロバイダーをインストールできます直接使用するため、アプリケーションが代わりに、Windows Sockets ダイレクトのテクノロジは、SAN サービス プロバイダーを使用して、この方法でサポートしていません。 アプリケーションによって直接使用するためにインストールされている SAN サービス プロバイダーは、TCP/IP プロトコルのものではなく、ネイティブのアドレス ファミリとプロトコルの特性をエクスポートします。

Windows Sockets スイッチを使ってアプリケーションに直接公開されている SAN サービス プロバイダーは、PFL を設定する必要があります\_で非表示フラグ、 **dwProviderFlags**の SAN サービス プロバイダーのメンバー [ **WSAPROTOCOL\_INFOW** ](https://msdn.microsoft.com/library/windows/hardware/ff565963)構造体。 オペレーティング システムの SAN サービス プロバイダーをインストール、SAN サービス プロバイダーのインストール メカニズムへの呼び出しでこの構造体を渡します、 **WSCInstallProvider**関数。 詳細については**WSCInstallProvider**、Microsoft Windows SDK のドキュメントを参照してください。 SAN サービス プロバイダーのインストール メカニズムは、たとえば、セットアップ プログラムまたは関数、SAN サービス プロバイダーがエクスポートされ、INF ファイルのディレクティブによって呼び出されます。

SAN サービス プロバイダーのインストール メカニズムはレジストリの型の値を追加する必要があります\_で SAN サービス プロバイダーを検出できる前に、レジストリで次のキーをバイナリ ベースの Windows Sockets サービス プロバイダーとしての Windows Sockets スイッチします。

```Console
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Winsock\
Parameters\TCP on SAN
```

この値は、値のバイナリ表現を含む、 **ProviderId** 、WSAPROTOCOL からメンバー\_INFOW 構造体。 この値は、Windows Sockets スイッチを使用した SAN サービス プロバイダーを登録します。 このメンバーには、仕入先が、SAN サービス プロバイダーに割り当てられているグローバル一意識別子 (GUID) が含まれています。

仕入先では、この GUID を表す一意の名前を割り当てることができますも。

-   製品の商標の名前

-   一意の数値

-   GUID のテキスト表現

**SAN サービス プロバイダーを登録するには**

1.  スイッチの呼び出し、 **WSAProviderConfigChange** Windows Sockets プロバイダーのインストールと削除イベントを検出する関数。

2.  新しい Windows Sockets サービス プロバイダーがインストールされているスイッチは呼び出し、 **WSCEnumProtocols**関数 Windows Sockets カタログと判断する、レジストリの SAN サービス プロバイダーの一覧を照会するかどうか、新しいサービスプロバイダーは、SAN を制御します。 詳細については**WSCEnumProtocols**、Windows SDK を参照してください。

3.  スイッチが」の説明に従ってそのサービス プロバイダーを初期化、スイッチは、新しい SAN サービス プロバイダーが検出される場合[SAN サービス プロバイダーの初期化](initializing-a-san-service-provider.md)します。

4.  スイッチは、ワイルドカードの IP アドレス (0.0.0.0) に、既存のリッスン ソケットがバインドされているサービスに SAN サービス プロバイダーが初期化された後も、新しくインストールされた SAN サービス プロバイダーの次の関数を呼び出します (ことを意味するワイルドカードの IP アドレス、SANサービス プロバイダーが着信要求を受け入れる接続制御のすべての Nic から)。

    <a href="" id="wspsocket"></a>**WSPSocket**  
    ソケットを作成します。

    <a href="" id="wspbind"></a>**WSPBind**  
    ワイルドカードの IP アドレスにソケットをバインドします。

    <a href="" id="wsplisten"></a>**WSPListen**  
    セットをそのスイッチによって受け入れられるまで、ソケットを認識し、キューに着信接続要求します。

    **注**  以降 Windows Vista では、ワイルドカードの IP アドレス 0.0.0.0 ご利用いただけません。
    また、Windows Vista で始まる場合、 **IPAutoconfigurationEnabled**レジストリ キーが値を 0 に設定、IP アドレスの自動割り当てを無効にすると、および IP アドレスが割り当てられていません。 ここで、 **ipconfig**コマンド ライン ツールでは、IP アドレスは表示されません。 キーが 0 以外の値に設定されている場合は、IP アドレスが自動的に割り当てられます。 このキーはレジストリに次のパスにすることはできます。

    **HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\IPAutoconfigurationEnabled**

    **HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\インターフェイス\\*GUID*\\IPAutoconfigurationEnabled**

     

 

 





