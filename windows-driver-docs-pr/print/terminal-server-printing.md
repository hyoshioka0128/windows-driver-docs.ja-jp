---
title: ターミナル サーバーの印刷
description: ターミナル サーバーの印刷
ms.assetid: 627d05f6-1499-4645-ad9a-b1a09f41b0c9
keywords:
- プリンター ドライバー WDK、ターミナル サーバー
- ターミナル サーバーの WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74cb02a357bacca18ee00d08559d9a1b339db193
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372360"
---
# <a name="terminal-server-printing"></a>ターミナル サーバーの印刷





Microsoft Windows 2000 以降では、ターミナル サービスを 1 台のサーバー システムに接続する複数のユーザーをできるようにするテクノロジをサポートします。 このサーバーのシステムには、ターミナル サーバーは呼び出されます。 ターミナル サービスの詳細については、Windows SDK のドキュメントを参照してください。

プリンター ミニドライバーまたは Windows 2000 またはそれ以降のドライバーを開発している場合は、ターミナル サーバーに接続されているプリンターをサポートするために特別な処理を実行する必要はありません。 ただし、Windows Driver Kit (WDK) で指定されたすべての設計、実装、およびインストールのガイドラインに従う必要があります。 具体的には、次の規則を使用する必要があります。

-   可能であれば、次の Microsoft 提供のドライバーのいずれかで動作するミニドライバーを用意するだけで、プリンターをサポートしてください。

    [Microsoft XPS プリンター ドライバー](xpsdrv-printer-driver.md)

    [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md)

    [Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md)

    [Microsoft プロッター ドライバー](microsoft-plotter-driver.md)

-   Windows Vista では、プリンター グラフィックス ユーザー モードで実行するための DLL を設計する必要があります。 参照してください[ユーザー モードまたはカーネル モードの選択](choosing-user-mode-or-kernel-mode.md)します。

-   デバイスは、カスタム ドライバーによってサポートされている必要がある場合に、ドライバーが Microsoft's に正確に従う必要があります[プリンター ドライバーのアーキテクチャ](printer-driver-architecture.md)します。 具体的には、次のとおりです。
    1.  作成する必要があります、[プリンター インターフェイス DLL](printer-interface-dll.md)します。
    2.  作成する必要があります、[プリンター グラフィックス DLL](printer-graphics-dll.md)します。 この DLL は、ユーザー モードまたはカーネル モードのいずれかで実行できますが、ユーザー モードをお勧めします。
    3.  カーネル モード コードを作成する場合を使用してコードをテストする必要があります[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。
    4.  」の説明に従って、セットアップ INF ファイルに基づくインストール手順を提供する必要があります[のインストールと構成のプリンター ドライバー](installing-and-configuring-printer-drivers.md)します。

すべてのカスタム ドライバー コードは、再入可能である必要があります。 ユーザー モードのコードでは、クリティカル セクション オブジェクトの (Windows SDK のドキュメントで説明) を使用する必要があります。 カーネル モード コードは、セマフォを使用する必要があります (を参照してください[ **EngCreateSemaphore** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatesemaphore)および関連する関数)。

プリンター ドライバーとカスタム スプーラー コンポーネントする必要がありますレジストリへのアクセス、これらのドライバーとスプーラー コンポーネントの場合は、専用のインターフェイスを介してのみ、WDK の適切なセクションで説明します。

### <a name="installation-considerations"></a>インストールに関する考慮事項

ユーザーが呼び出すときに、Microsoft のプリンター クラスのインストーラーによって読み取ることができる INF ファイルを指定のインストールを行う必要があるすべては、通常、**プリンターの追加**ウィザード。 場合によっては、カスタム セットアップ コード (共同インストーラーまたはクラスのインストーラー) はも必要です。 カスタム セットアップ コードを作成する必要がある場合、次に注意してください。

-   ユーザーまたはセットアップ コードは、ターミナル サーバーをインストール モードに切り替える必要があります。 (詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

-   システム ファイルを置換しようとしないでください。 Windows ファイル保護には、システム ファイルの置換が禁止されています。

-   可能な限りシステムの再起動を要求しないでください。 次のガイドラインに従ってください。
    1.  ドライバー ファイルが変更されていないことを置き換えないでください。 たとえば、いくつかのデバイスで共有されるファイルは、最新バージョンが既にインストールされている場合にいない更新する必要があります。
    2.  ファイルを置き換える必要がある場合、セットアップ コードは、古いバージョンをアンロードし、(たとえば、サービスを再起動し、ファイルを置き換える、ドライバー サービスを停止する) を新しいバージョンを読み込む手順を実行する必要があります。
    3.  再記録オフ ログオンするユーザーを要求するには、はシステムの再起動を必要とすることをお勧めします。

共同インストーラーとクラスのインストーラーの詳細については、次を参照してください。[クラスのインストーラーを執筆および共同インストーラー](https://docs.microsoft.com/windows-hardware/drivers/install/writing-class-installers-and-co-installers)します。

**注**  カスタム セットアップ コードを記述する前に、Windows SDK のドキュメントで説明するガイドラインをプログラミングするターミナル サービスを読み取る必要があります。

 

### <a name="user-interface-considerations"></a>ユーザー インターフェイスに関する考慮事項

ユーザーによって実行されるカスタム セットアップ コードは、ユーザー インターフェイスを表示できます。

ほぼすべてのプリンター ドライバーのコードでは、スプーラーの実行コンテキストで実行され、そのため、ユーザー インターフェイスを表示することはできません。 プリンター インターフェイス Dll、およびのみ内からのみ、ユーザー インターフェイスが表示されることができます、次の機能。

-   [ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets)と[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)関数で、プロパティ ページを作成します。

-   [ **DrvPrinterEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)関数で、プリンターのイベントを識別するイベント コードを受信します。 関数が、プリンターに対してのみユーザー インターフェイスを表示できます\_イベント\_追加\_接続とプリンターの\_イベント\_削除\_イベント コードを接続します。

その他のすべてのプリンター ドライバーのコードは、スプーラーのコンテキストで実行します。 このコンテキストから呼び出し**メッセージ ボックス**または**MessageBoxEx**が許可されている MB に設定する必要がありますが、\_サービス\_通知。 これらの関数は、Windows SDK のドキュメントで説明します。

 

 




