---
title: ネットワーク コンポーネントのインストールに使用されるコンポーネントとファイル
description: ネットワーク コンポーネントのインストールに使用されるコンポーネントとファイル
ms.assetid: be056ff1-0b92-4e81-a506-7750012aad4e
keywords:
- ネットワーク コンポーネント コンポーネントおよびファイルの使用、WDK をインストールします。
- ネットワーク コンポーネントのインストール コンポーネントと使用するファイルの WDK
- WDK のネットワーク インストールのコンポーネント
- クラスのインストーラーの WDK ネットワーク
- WDK ネットワークの共同インストーラー
- DLL の WDK のネットワーク移行
- テキスト モードのセットアップの WDK ネットワーク
- ドライバーのイメージ ファイルの WDK ネットワーク
- ドライバー ライブラリ ファイルの WDK ネットワーク
- DLL の WDK ネットワークの移行
- ベンダーから提供されたインストール ファイルの WDK ネットワーク
- ファイルの WDK ネットワーク コンポーネントがインストールされます。
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8afc447883bb2953874275c57d7db0a1c31089ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379264"
---
# <a name="components-and-files-used-for-network-component-installation"></a>ネットワーク コンポーネントのインストールに使用されるコンポーネントとファイル

次のコンポーネントとファイルは、ネットワーク ドライバーをインストールするに使用されます。

-   1 つ以上の情報 (INF) ファイル

-   必要なクラスのインストーラーと、ミニポート ドライバーの省略可能な共同インストーラー

-   INetCfg のプロトコルとフィルター ドライバー

-   省略可能な通知オブジェクト

1 つ以上の前のコンポーネント、だけでなく仕入先はまた、必要に応じて、次のファイルを提供します。

-   1 つまたは複数のデバイス ドライバー (.sys) のイメージ ファイルおよびドライバー ライブラリ (.dll) ファイル

-   ドライバー カタログのファイル

-   テキスト モードのセットアップ情報ファイル (txtsetup.oem)

## <a name="inf-files"></a>INF ファイル

各ネットワーク コンポーネント、コンポーネントをインストールするネットワーク クラスのインストーラーを使用する情報 (INF) ファイルが必要です。 ネットワークの INF ファイルは、共通の INF ファイル形式に基づいています。 INF ファイルの形式に関する詳細については、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

ネットワーク コンポーネントの INF ファイルの作成の詳細については、次を参照してください。[ネットワーク INF ファイルの作成](creating-network-inf-files.md)です。

## <a name="inetcfg"></a>INetCfg

呼び出すことによってこれらの NDIS プロトコルとフィルター ドライバーがインストールされている現在、`INetCfg`ファミリの[構成のネットワーク インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v=vs.85))します。 たとえば、ネットワークのコンポーネントをインストールまたは削除、ドライバー ライターを呼び出すには[INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709(v=vs.85))インターフェイス。 

ドライバー作成者がこのインターフェイスのいずれかの呼び出しをプログラムでできますか、使用できる[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)、呼び出す`INetCfg`代わりにします。

プロトコル ドライバーのインストールの詳細については、次を参照してください。 [NDIS ドライバーのインストールのプロトコル](ndis-protocol-driver-installation.md)します。

フィルター ドライバーのインストールの詳細については、次を参照してください。 [NDIS フィルター ドライバーのインストール](ndis-filter-driver-installation.md)します。

## <a name="notify-object"></a>オブジェクトへの通知します。

ネットワーク プロトコル、クライアント、またはサービスなどのソフトウェア コンポーネントを持つことができます、*通知オブジェクト*します。 通知オブジェクトは、ユーザー インターフェイスを表示、イベントをバインドできるように、コンポーネント、バインディング プロセスをいくつかの制御し条件付きでインストールまたは削除できるソフトウェア コンポーネントのコンポーネントに通知できます。 詳細については、オブジェクトに通知を参照してください[ネットワーク コンポーネントの通知オブジェクト](notify-objects-for-network-components.md)します。

ネットワーク アダプターには、通知オブジェクトを含めることはできません。 共同インストーラーことができます。 共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](https://docs.microsoft.com/windows-hardware/drivers/install/writing-a-co-installer)です。

## <a name="vendor-supplied-files"></a>ベンダーから提供されたファイル

仕入先には、通常のドライバー (.sys) のイメージ ファイルとドライバー ライブラリ (.dll) ファイルで構成されると、デバイスの 1 つまたは複数のドライバーが用意されています。 仕入先がオプションのドライバーを指定しても*カタログ ファイル*します。 仕入先は、そのドライバー パッケージのテストと署名 Windows Hardware Quality Lab (WHQL) に送信することで、デジタル署名を取得します。 WHQL は、カタログ (.cat) ファイルを使用して、パッケージを返します。 仕入先は、デバイスの INF ファイルで、カタログ ファイルを一覧表示する必要があります。

省略可能なテキスト モードのセットアップ情報ファイル (txtsetup.oem) は、ベンダーによっても指定することがあります。 ネットワーク デバイスは、マシンを起動する必要は、か、オペレーティング システムのキットでは、ドライバーまたはデバイスのドライバーを含める必要があるようなデバイスのベンダーに txtsetup.oem ファイルを提供する必要があります。 Txtsetup.oem ファイルには、テキスト モードのセットアップ中にデバイスをインストールするセットアップのシステム コンポーネントによって使用される情報が含まれています。

 

 





