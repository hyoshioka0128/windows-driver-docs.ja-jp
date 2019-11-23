---
title: ターミナル サーバーの印刷
description: ターミナル サーバーの印刷
ms.assetid: 627d05f6-1499-4645-ad9a-b1a09f41b0c9
keywords:
- プリンタードライバー WDK、ターミナルサーバー
- ターミナルサーバー印刷 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f81a0ce66f484174f263796ed538e092b9a00d6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838781"
---
# <a name="terminal-server-printing"></a>ターミナル サーバーの印刷





Microsoft Windows 2000 以降では、複数のユーザーが単一のサーバーシステムに接続できるようにするテクノロジであるターミナルサービスがサポートされています。 このサーバーシステムは、ターミナルサーバーと呼ばれます。 ターミナルサービスの詳細については、Windows SDK のドキュメントを参照してください。

Windows 2000 以降のプリンターミニドライバーまたはドライバーを開発している場合は、ターミナルサーバーに接続されているプリンターをサポートするために特別な操作を行う必要はありません。 ただし、Windows Driver Kit (WDK) に指定されているすべての設計、実装、およびインストールのガイドラインに従う必要があります。 具体的には、次の規則を使用する必要があります。

-   可能であれば、次の Microsoft 提供のドライバーのいずれかで動作するミニドライバーを提供するだけで、プリンターをサポートします。

    [Microsoft XPS プリンタードライバー](xpsdrv-printer-driver.md)

    [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md)

    [Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md)

    [Microsoft プロッター ドライバー](microsoft-plotter-driver.md)

-   Windows Vista では、ユーザーモードで実行するようにプリンターグラフィックス DLL を設計する必要があります。 「[ユーザーモードまたはカーネルモードの選択](choosing-user-mode-or-kernel-mode.md)」を参照してください。

-   デバイスがカスタムドライバーでサポートされている必要がある場合は、ドライバーが Microsoft の[プリンタードライバーのアーキテクチャ](printer-driver-architecture.md)に厳密に準拠している必要があります。 具体的には、次のとおりです。
    1.  [プリンターインターフェイス DLL](printer-interface-dll.md)を作成する必要があります。
    2.  [プリンターグラフィックス DLL](printer-graphics-dll.md)を作成する必要があります。 この DLL は、ユーザーモードまたはカーネルモードで実行できますが、ユーザーモードをお勧めします。
    3.  カーネルモードコードを作成する場合は、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用してコードをテストする必要があります。
    4.  「[プリンタードライバーのインストールと構成](installing-and-configuring-printer-drivers.md)」で説明されているように、セットアップの INF ファイルに基づいてインストール手順を指定する必要があります。

すべてのカスタムドライバーコードは再入可能である必要があります。 ユーザーモードのコードでは、重要なセクションオブジェクト (Windows SDK のドキュメントで説明) を使用する必要があります。 カーネルモードのコードでは、セマフォを使用する必要があります (「 [**EngCreateSemaphore**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatesemaphore) and related functions」を参照してください)。

プリンタードライバーおよびカスタムスプーラコンポーネントは、WDK の該当するセクションで説明されているように、これらのドライバーおよびスプーラコンポーネント専用のインターフェイスを介してのみレジストリにアクセスする必要があります。

### <a name="installation-considerations"></a>インストールに関する考慮事項

通常、インストールに必要なのは、ユーザーが**プリンターの追加**ウィザードを起動したときに Microsoft のプリンタークラスインストーラーが読み取ることができる INF ファイルです。 カスタムセットアップコード (共同インストーラーまたはクラスインストーラー) も必要になる場合があります。 カスタムセットアップコードを作成する必要がある場合は、次の点に注意してください。

-   ユーザーまたはセットアップコードがターミナルサーバーをインストールモードにする必要があります。 (詳細については、Microsoft Windows SDK のドキュメントを参照してください)。

-   システムファイルの置換を試行しないでください。 Windows ファイル保護では、システムファイルの置換が禁止されています。

-   システムの再起動をできるだけ避けてください。 次のガイドラインに従ってください。
    1.  変更されていないドライバーファイルは置き換えないでください。 たとえば、最新バージョンが既にインストールされている場合、複数のデバイスで共有されているファイルを更新することはできません。
    2.  ファイルを置き換える必要がある場合は、セットアップコードで古いバージョンをアンロードしてから新しいバージョンを読み込む必要があります (たとえば、ドライバーサービスを停止し、ファイルを置き換え、サービスを再起動します)。
    3.  システムの再起動を必要とする場合は、ユーザーがログオフしてから再度ログオンする必要があります。

共同インストーラーとクラスインストーラーの詳細については、「[クラスインストーラーと共同インストーラーの記述](https://docs.microsoft.com/windows-hardware/drivers/install/writing-class-installers-and-co-installers)」を参照してください。

**メモ**   カスタムセットアップコードを記述する前に、Windows SDK のドキュメントに記載されているターミナルサービスのプログラミングガイドラインを読むことが重要です。

 

### <a name="user-interface-considerations"></a>ユーザーインターフェイスに関する考慮事項

ユーザーが実行するカスタムセットアップコードでは、ユーザーインターフェイスを表示できます。

ほとんどすべてのプリンタドライバコードはスプーラの実行コンテキストで実行されるため、ユーザーインターフェイスを表示することはできません。 ユーザーインターフェイスを表示できるのは、プリンターインターフェイス Dll だけで、次の関数の中からだけです。

-   [**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)関数と[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数。プロパティページを作成します。

-   [**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数。プリンターイベントを識別するイベントコードを受け取ります。 関数は、PRINTER\_イベントに対してのみユーザーインターフェイスを表示できることに注意してください\_接続とプリンターの\_イベント\_追加して\_接続イベントコードを削除します。\_

その他のすべてのプリンタードライバーコードは、スプーラのコンテキストで実行されます。 このコンテキストでは、 **MessageBox**または**messageboxex**を呼び出すことができますが、MB\_サービス\_通知を設定する必要があります。 これらの関数については、Windows SDK のドキュメントを参照してください。

 

 




