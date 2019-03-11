---
title: WDK の以前のバージョンとその他のダウンロード
description: Windows Driver Kit (WDK)、Windows デバッガー (WinDBG) などの各バージョンをインストールします。
ms.assetid: e07d9f05-f8d0-46e5-82e6-c23baa614bb1
keywords:
- Windows Driver Kit (WDK)
- 以前のバージョン
- WDK
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0515bb2812a30a27c8f6a5c5d0a2c69a10777c3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518952"
---
# <a name="other-wdk-downloads"></a>その他の WDK のダウンロード

ドライバーの開発には、[Windows Driver Kit (WDK) と各ツールの最新の公開バージョン](download-the-wdk.md)を使用してください。 このトピックは、WDK の以前のバージョンと追加のダウンロードに関する情報を、サポート目的に提供するものです。


## <a name="wdk-for-windows-10-version-1803"></a>WDK for Windows 10 Version 1803

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2017 のインストール 
Visual Studio 2017 の次のエディションでドライバー開発がサポートされています。 

* [Visual Studio Community 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [Visual Studio Professional 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [Visual Studio Enterprise 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

Visual Studio のインストール時に、**[C++ によるデスクトップ開発]** ワークロードを選びます。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 

ARM/ARM64 ドライバーを開発するには、**[個別のコンポーネント]** を選び、**[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選びます。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1803"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 Version 1803 のインストール

* [WDK for Windows 10 Version 1803 のダウンロード](https://go.microsoft.com/fwlink/?linkid=873060) 

1709 リリースの新機能:WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 WDK VS 統合が機能するためには、この拡張機能をインストールする必要があります。 

## <a name="enterprise-wdk-for-windows-10-version-1803-ewdk"></a>Enterprise WDK for Windows 10 Version 1803 (EWDK) 

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio Build Tools 15.7 が含まれています。 まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-157"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools 15.7

* [EWDK for Windows 10 Version 1803 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-EWDK)

## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-run-time-requirements"></a>リリース ノートと実行時の要件

WDK には Visual Studio が必要です。Visual Studio に関するシステム要件について詳しくは、[Visual Studio 2017 のシステム要件](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)に関する記事をご覧ください。 

EWDK では、さらに .NET 4.6.1 も必要になります .NET を実行するための要件について詳しくは、[.NET Framework のシステム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)に関する記事をご覧ください。 

HAL 拡張機能を操作するには、開発用の環境を準備した後に、更新された [Windows OEM HAL Extension Test Cert 2017 (テストのみ)](https://go.microsoft.com/fwlink/?linkid=872294) の証明書をダウンロードしてインストールします。  [詳細情報](https://support.microsoft.com/help/4131991)


## <a name="wdk-for-windows-10-version-1709"></a>WDK for Windows 10 Version 1709

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2017 のインストール 
Visual Studio 2017 の次のエディションでドライバー開発がサポートされています。 

* [Visual Studio Community 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [Visual Studio Professional 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [Visual Studio Enterprise 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

Visual Studio のインストール時に、**[C++ によるデスクトップ開発]** ワークロードを選びます。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 

ARM/ARM64 ドライバーを開発するには、**[個別のコンポーネント]** を選び、**[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選びます。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1709"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 Version 1709 のインストール

* [WDK for Windows 10 Version 1709 のダウンロード](https://go.microsoft.com/fwlink/p/?linkid=859232) 

このリリースの新機能:WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 WDK VS 統合が機能するためには、この拡張機能をインストールする必要があります。 

## <a name="enterprise-wdk-for-windows-10-version-1709-ewdk"></a>Enterprise WDK for Windows 10 Version 1709 (EWDK) 

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio Build Tools 15.6 が含まれています。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-156-recommended"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools 15.6 (推奨)

* [EWDK for Windows 10 Version 1709 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-6)

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-154"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools 15.4

* [EWDK for Windows 10 Version 1709 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-4)

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools-152"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools 15.2

* [EWDK for Windows 10 Version 1709 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709)

まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。

## <a name="wdk-for-windows-10-version-1703"></a>WDK for Windows 10 Version 1703 

### <a name="download-iconimagesdownload-installpng-install-visual-studio-2015"></a>![ダウンロード アイコン](images/download-install.png) Visual Studio 2015 のインストール

> [!IMPORTANT]
> WDK for Windows 10 Version 1703 は、まだ Visual Studio 2017 と互換性がありません。 このバージョンの WDK を使ってドライバーを開発する場合は、Visual Studio 2015 を使用してください。 

ドライバー開発は、Visual Studio 2015 の以下のエディションでサポートされます。 

* [Visual Studio Express 2015 for Desktop のダウンロード](https://go.microsoft.com/fwlink/?linkid=875331)
* [Visual Studio Community 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=534599)
* [Visual Studio Professional 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=619628)
* [Visual Studio Enterprise 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=619629)

### <a name="download-iconimagesdownload-installpng-install-windows-sdk-for-windows-10-version-1703"></a>![ダウンロード アイコン](images/download-install.png) Windows SDK for Windows 10 Version 1703 のインストール 

* [Windows SDK for Windows 10 Version 1703 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=845298)

### <a name="download-iconimagesdownload-installpng-install-wdk-for-windows-10-version-1703"></a>![ダウンロード アイコン](images/download-install.png) WDK for Windows 10 Version 1703 のインストール 

* [WDK for Windows 10 Version 1703 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=845980)

> [!IMPORTANT]
> WDK をインストールすると、モダン アプリケーションを開発することができなくなります。 

> [!IMPORTANT]
> WDK for Windows 10 Version 1607 がインストールされている場合に、WDK for Windows 10 Version 1703 を WDK for Windows 10 Version 1607 に上書きインストールすると、一部の WDK ファイルが削除されます。 これらのファイルを復元するには、次を行います。 
> 1. スタート メニューで、検索ボックスに「**アプリと機能**」と入力し、検索結果から **[アプリと機能]** を選択します。 
> 2. **[アプリと機能]** の一覧で、"**Windows Driver Kit - Windows 10.0.15063.0**" を探し、そのプログラムを選びます。 
> 3. **[変更]**、**[修復]** の順に選び、画面の指示に従います。 
> 4. ファイルが復元されます。 

## <a name="download-iconimagesdownload-installpng-ewdk-for-windows-10-version-1703"></a>![ダウンロード アイコン](images/download-install.png) EWDK for Windows 10 Version 1703 

EWDK をインストールして、コマンド ライン ビルド環境で、ドライバーや基本的な Win32 テスト アプリケーションを構築することもできます。 ただしこの環境には、統合開発環境 (IDE) など、Visual Studio で利用可能なすべての機能が用意されているわけではないため、任意のコード エディターを使用する必要があります。 

* [EWDK について詳しく知る](https://go.microsoft.com/fwlink/p/?LinkId=846040)
* [EWDK for Windows 10 Version 1703 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1703)


## <a name="download-iconimagesdownload-installpng-wdk-for-windows-10-version-1607"></a>![ダウンロード アイコン](images/download-install.png) EWDK for Windows 10 Version 1607 のダウンロード

1. Windows Update を実行します。 
2. 開発ニーズに最適なバージョンの Visual Studio 2015 をインストールします。 

    * [Visual Studio Express 2015 for Desktop のダウンロード](https://go.microsoft.com/fwlink/?linkid=875331)
    * [Visual Studio Community 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=534599)
    * [Visual Studio Professional 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=619628)
    * [Visual Studio Enterprise 2015 のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=619629)

3. インストール時には、**[Windows 10 開発者の標準]** オプションを選択してください。 
4. 画面に表示される指示に従って、インストールを完了します。 
5. [Windows 10 バージョン 1607 用 WDK をインストール](https://go.microsoft.com/fwlink/p/?LinkId=526733) 
**するか、**
[EWDK 1607 をインストール](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk)します

## <a name="download-iconimagesdownload-installpng-wdk-81-update-for-windows-81-8-and-7-drivers"></a>![ダウンロード アイコン](images/download-install.png) WDK 8.1 Update (Windows 8.1、8、7 ドライバー用)

WDK 8.1 Update には、Windows 8.1 Update、Windows 8.1、Windows 8、Windows 7 向けのドライバーを構築、テスト、デバッグ、展開するためのツールが含まれています。 WDK をイントールしたら、WDK 8.1 Update Test Pack をインストールすることをお勧めします。 このパッケージには、デバイスの基本機能、グラフィックス、イメージング、モバイル ブロードバンド (CDMA、GSM、WLAN)、センサー、その他のユーティリティに対するテストが用意されています。 

> [!IMPORTANT]
> WDK 8.1 Update をインストールする前に Visual Studio 2013 をインストールする必要があります。 

1. [Visual Studio 2013 のダウンロード](https://go.microsoft.com/fwlink/?linkid=875331)
2. [WDK 8.1 Update のダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=393659) (英語のみ) 
3. [WDK 8.1 Update Test Pack のダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=393660) (英語のみ) 
4. [Windows 8.1 向けのドライバー サンプルを入手する](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-81-cf35e953) 

## <a name="download-iconimagesdownload-installpng-windbg-for-windows-81"></a>![ダウンロード アイコン](images/download-install.png) Windows 8.1 向け WinDbg
Windows 向けデバッグ ツール (WinDbg) は WDK 8.1 Update に含まれていますが、スタンドアロン コンポーネントとして Windows 8.1 SDK からインストールすることもできます。 インストール ウィザードで、Windows 向けデバッグ ツールを選び、それ以外のすべてのコンポーネントの選択を解除します。 

* [Windows 8.1 SDK の一部として (WinDbg) を入手](https://go.microsoft.com/fwlink/p/?LinkId=323507) (英語のみ)

## <a name="download-iconimagesdownload-installpng-remote-debugging-client-for-windows-81"></a>![ダウンロード アイコン](images/download-install.png) Windows 8.1 向けリモート デバッグ クライアント
Windows リモート デバッグ クライアントを使うと、Microsoft の開発者とインターネットを介してリモートで連携し、カーネル モードの問題をカーネル デバッガーを使ってデバッグすることができます。 
* [リモート デバッグの詳細と準備については、こちらをご覧ください](https://docs.microsoft.com/windows-hardware/drivers/debugger/remote-debugging)。
* [リモート デバッグ クライアントをダウンロードする](https://go.microsoft.com/fwlink/p/?LinkId=316921) (英語のみ)  

## <a name="download-iconimagesdownload-installpng-wdk-8"></a>![ダウンロード アイコン](images/download-install.png) WDK 8
WDK 8 を使用すると、以前のドライバーを WDK 8.1 Update と Visual Studio 2013 に移行できます。 WDK 8 はサポートされないため、このキットの更新プログラムは提供されません。 WDK と Visual Studio の最新バージョンを使って Windows 用ドライバーをビルドしてください。 

> [!IMPORTANT]
> WDK 8 をインストールする前に、[Visual Studio Professional 2012](https://go.microsoft.com/fwlink/p/?LinkID=255976) または [Visual Studio Ultimate 2012](https://go.microsoft.com/fwlink/p/?LinkID=255982) をインストールする必要があります。 

1. [WDK 8 のダウンロード (英語のみ)](https://go.microsoft.com/fwlink/p/?LinkID=324284)
2. [WDK 8 再頒布可能コンポーネントのダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=253170) (英語のみ) 
3. [Windows 8 向けのドライバー サンプルを入手](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-80-e3161626) 

## <a name="download-iconimagesdownload-installpng-wdk-710-for-windows-xp-drivers"></a>![ダウンロード アイコン](images/download-install.png) WDK 7.1.0 (Windows XP ドライバー用)
Windows XP または Windows Server 2003 向けドライバーの開発 WDK 7.1.0 には、これらのオペレーティング システム用のドライバーを作るために使うことができるツール、コード サンプル、ドキュメント、コンパイラ、ヘッダー、ライブラリがあります。 

* [WDK 7.1.0 のダウンロード](https://www.microsoft.com/download/confirmation.aspx?id=11800) (英語のみ) 

## <a name="download-iconimagesdownload-installpng-standalone-debugging-tools-for-debugging-windows-xp-and-windows-vista"></a>![ダウンロード アイコン](images/download-install.png) スタンドアロンのデバッグ ツール (Windows XP と Windows Vista のデバッグ用)
Windows XP、Windows Server 2003、Windows Vista、または Windows Server 2008 をデバッグしている場合 (またはこれらのオペレーティング システムのいずれかを使って Debugging Tools for Windows を実行している場合) は、デバッグ ツールの Windows 7 リリースを使う必要があります。 これは、Windows 7 と .NET Framework 4.0 用 SDK に含まれています。 Windows 向けデバッグ ツールをスタンドアロン コンポーネントとしてインストールするには、SDK インストール ウィザードで Windows 向けデバッグ ツールを選び、他のすべてのコンポーネントを選択解除します。 

> [!IMPORTANT]
> SDK for Windows 7 をインストールする際に、新しいバージョンの Visual C++ 2010 再頒布可能パッケージによって問題が発生することがあります。 詳しくは、[Windows SDK のサポートのページ](https://support.microsoft.com/kb/2717426)をご覧ください。 

* [スタンドアロンの Windows XP 用デバッグ ツールを Windows 7 SDK の一部として入手する](https://www.microsoft.com/download/confirmation.aspx?id=8279) 

## <a name="related-downloads"></a>関連するダウンロード
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [Windows HLK、HCK、Logo Kit のダウンロード](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit) 
* [Windows 向けデバッグ ツール (WinDbg) のダウンロード](https://developer.microsoft.com/windows/hardware/download-windbg) 
* [Windows シンボル パッケージのダウンロード](https://developer.microsoft.com/windows/hardware/download-symbols) 
* [WDK Insider Preview のダウンロード](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK) 
