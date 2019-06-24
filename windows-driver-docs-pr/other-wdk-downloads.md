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
ms.custom: 19H1
ms.openlocfilehash: 97ebdb06db555331f2a41700acddf4e76b0ad9d7
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63373555"
---
# <a name="other-wdk-downloads"></a>その他の WDK のダウンロード

このトピックでは、以前のバージョンの Windows Driver Kit (WDK)、Enterprise WDK (EWDK)、および追加のダウンロードに関する情報をサポート目的で提供します。 ドライバーを開発するには、最新の公開バージョンの Windows Driver Kit (WDK) とツールを使用します (「[Windows Driver Kit (WDK) のダウンロード](download-the-wdk.md)」からダウンロード可能)。

Windows Driver Kit (WDK) は、Windows ドライバーの開発、テスト、展開に使用します。 ドライバーを開発するには、最新の公開バージョンの Windows Driver Kit (WDK) とツールを使用します (「[Windows Driver Kit (WDK) のダウンロード](download-the-wdk.md)」からダウンロード可能)。

このトピックでは、以前のバージョンの WDK、Enterprise WDK (EWDK)、および追加のダウンロードに関する情報をサポート目的で提供します。 以前のバージョンを使用するには、*まず*対象プラットフォームに適した Visual Studio のバージョンをインストールする必要があります。

## <a name="step-1-install-visual-studio"></a>手順 1:Visual Studio をインストールする

ドライバーの開発は、Visual Studio の特定のバージョンでサポートされています。 Windows の特定バージョン用のドライバーを開発するには、次の表で指定されて (ダウンロード用にリンクされて) いるいずれかのバージョンの Visual Studio を使用する必要があります。

| Windows の対象バージョン      | Visual Studio のエディション            |
|--------------------------|----------------------------------------|
| Windows 10 Version 1809 <br/>Windows 10 バージョン 1803 <br/>Windows 10 バージョン 1709 | [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15) <br/>[Visual Studio Professional 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) <br/>[Visual Studio Enterprise 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15) |
| Windows 10 Version 1703 <br/>Windows 10 Version 1607 | [Visual Studio Express 2015 for Desktop](https://go.microsoft.com/fwlink/?linkid=875331) <br/>[Visual Studio Community 2015](https://go.microsoft.com/fwlink/p/?LinkId=534599) <br/>[Visual Studio Professional 2015](https://go.microsoft.com/fwlink/p/?LinkId=619628) <br/>[Visual Studio Enterprise 2015](https://go.microsoft.com/fwlink/p/?LinkId=619629) |
| Windows 8.1 Update <br/>Windows 8.1 | [Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=875331) |
| Windows 8                | [Visual Studio Professional 2012](https://go.microsoft.com/fwlink/p/?LinkID=255976) <br/>[Visual Studio Ultimate 2012](https://go.microsoft.com/fwlink/p/?LinkID=255982) |

### <a name="configure-visual-studio-for-windows-10-versions-1709-1803-and-1809"></a>Windows 10 バージョン 1709、1803 および 1809用の Visual Studio を構成する

Visual Studio のインストール時に、 **[C++ によるデスクトップ開発]** ワークロードを選びます。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。

ARM/ARM64 用のドライバーを開発するには、 **[個別のコンポーネント]** を選択し、 **[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選択します。

### <a name="install-the-windows-sdk-to-target-windows-10-versions-1607-and-1703"></a>Windows 10 バージョン 1607 および 1703 を対象とする Windows SDK をインストールする

Windows 10 バージョン 1607 または Windows 10 バージョン 1703 を実行するシステムを対象に開発する場合は、Visual Studio 2015 をインストールしてから、 次の表に指定されている対象の Windows 10 バージョン用の Windows SDK のバージョンをダウンロードしてインストールする必要があります。

| Windows の対象バージョン      | Windows SDK のバージョン            |
|--------------------------|----------------------------------------|
| Windows 10 Version 1703 | [Windows SDK for Windows 10.0.15063.468](https://go.microsoft.com/fwlink/p/?LinkID=845298) |
| Windows 10 Version 1607 | [Windows SDK for Windows 10.0.14393.795](https://go.microsoft.com/fwlink/p/?LinkId=838916) |
| Windows 8.1              | [Windows 8.1 向け Windows SDK](https://go.microsoft.com/fwlink/p/?LinkId=323507) |
| Windows 8                | [Windows SDK for Windows 8](https://go.microsoft.com/fwlink/p/?LinkId=226658) |

Visual Studio 2015 には Windows SDK が含まれていないため、SDK を個別にインストールする必要があります。 新しいバージョンの Visual Studio には Windows SDK が含まれています。

## <a name="step-2-install-the-wdk"></a>手順 2:WDK をインストールする

WDK は Visual Studio および Debugging Tools for Windows (WinDbg) と統合されています。 この統合された環境には、ドライバーの開発、構築、パッケージ、デプロイ、テスト、デバッグのために必要なツールが用意されています。

> [!Note]
> Windows 10 バージョン 1709 以降では、WDK をインストールすると Visual Studio の WDK 拡張機能が既定でインストールされます。 この拡張機能は、WDK と Visual Studio の統合のために必要です。

| Windows のバージョン      | WDK と関連するダウンロード                       |
|--------------------------|-------------------------------------------------|
| Windows 10 Version 1809 | [WDK for Windows 10 Version 1809](https://go.microsoft.com/fwlink/?linkid=2026156) |
| Windows 10 バージョン 1803 | [WDK for Windows 10 Version 1803](https://go.microsoft.com/fwlink/?linkid=873060) |
| Windows 10 バージョン 1709 | [WDK for Windows 10 Version 1709](https://go.microsoft.com/fwlink/p/?linkid=859232) |
| Windows 10 Version 1703 | [WDK for Windows 10 Version 1703](https://go.microsoft.com/fwlink/p/?LinkID=845980) |
| Windows 10 Version 1607 | [WDK for Windows 10 Version 1607](https://go.microsoft.com/fwlink/p/?LinkId=526733)                |
| Windows 8.1 Update       | [WDK 8.1 Update](https://go.microsoft.com/fwlink/p/?LinkId=393659) (英語のみ) <br/>[WDK 8.1 Update Test Pack](https://go.microsoft.com/fwlink/p/?LinkID=393660) (英語のみ) <br/>[WDK 8.1 サンプル](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-81-cf35e953) |
| Windows 8                | [WDK 8](https://go.microsoft.com/fwlink/p/?LinkID=324284) (英語のみ) <br/>[WDK 8 再頒布可能コンポーネント](https://go.microsoft.com/fwlink/p/?LinkID=253170) (英語のみ) <br/>[WDK 8 サンプル](https://code.msdn.microsoft.com/windowshardware/Windows-Driver-Kit-WDK-80-e3161626) |
| Windows XP <br/>Windows Server 2003 | [WDK 7.1.0](https://www.microsoft.com/download/confirmation.aspx?id=11800) |


> [!IMPORTANT]
> WDK for Windows 10 Version 1607 をインストール済みのシステムに、WDK for Windows 10 Version 1703 をインストールした場合、以前のバージョンの WDK の一部のファイルが削除される可能性があります。 これらのファイルを復元するには、次を行います。
> 1. スタート メニューで、検索ボックスに「**アプリと機能**」と入力し、検索結果から **[アプリと機能]** を選択します。
> 2. **[アプリと機能]** の一覧で、"**Windows Driver Kit - Windows 10.0.15063.0**" を探し、そのプログラムを選びます。
> 3. **[変更]** 、 **[修復]** の順に選び、画面の指示に従います。
> 4. ファイルが復元されます。

## <a name="optional-install-the-ewdk"></a>省略可能: EWDK のインストール

Enterprise WDK (EWDK) は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境であり、基本的な Win32 テスト アプリケーションです。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。 この環境には、統合開発環境 (IDE) など、Visual Studio で利用可能な一部の機能が含まれていません。

EWDK を使用するには、.NET Framework 4.6.1 が必要です。 このバージョンのフレームワークを実行するシステムの詳細については、「[.NET Framework のシステム要件](https://docs.microsoft.com/en-us/dotnet/framework/get-started/system-requirements)」を参照してください。 .NET Framework のダウンロード用リンクについては、「[開発者向けの .NET Framework のインストール](https://docs.microsoft.com/en-us/dotnet/framework/install/guide-for-developers)」を参照してください。

EWDK の詳細については、「[Enterprise WDK 10 の使用](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/using-the-enterprise-wdk)」を参照してください。

| Windows のバージョン               | EWDK                              |
|-----------------------------------|-----------------------------------|
| Windows 10 Version 1809          | [EWDK for Windows 10 Version 1809](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) |
| Windows 10 バージョン 1803          | [EWDK for Windows 10 Version 1803](https://developer.microsoft.com/windows/hardware/license-terms-EWDK) |
| Windows 10 バージョン 1709          | [EWDK for Visual Studio with Build Tools 15.6](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-6) (推奨) <br/>[EWDK for Visual Studio with Build Tools 15.4](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709-VS15-4) <br/>[EWDK for Visual Studio with Build Tools 15.2](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1709) |
| Windows 10 Version 1703          | [EWDK for Windows 10 Version 1703](https://developer.microsoft.com/windows/hardware/license-terms-enterprise-wdk-1703) |

> [!Note]
> Windows 10 バージョン 1709 以降、EWDK は ISO ベースです。ased. まず、ISO をダウンロードしてマウントした後、**LaunchBuildEnv** を実行します。

## <a name="optional-install-updated-test-certificates-for-hal-extensions"></a>省略可能: HAL 拡張機能の更新されたテスト証明書をインストールする

HAL 拡張機能を使用するには、Windows 10 バージョン 1709 または新しいバージョンの Windows 10 を実行している開発システムの準備を行います。 また、WDK または EWDK をインストールしてから、**Windows OEM HAL Extension Test Cert 2017 (テストのみ)** の更新されたバージョンをインストールします。これは、ZIP ファイルでダウンロードできます([HAL_Extension_Test_Cert_2017.zip](https://go.microsoft.com/fwlink/?linkid=872294))。

この更新された証明書の使用に関する詳細については、Windows サポートの「[Update for "Windows OEM HAL Extension Test Cert 2017 (TEST ONLY)" test certificate](https://support.microsoft.com/help/4131991)」("Windows OEM HAL Extension Test Cert 2017 (テストのみ)" のテスト証明書の更新) を参照してください。

## <a name="optional-install-windbg-preview"></a>省略可能: WinDbg Preview をインストールする

WinDbg Preview は、最新の外観、高速なウィンドウ、本格的なスクリプトの操作性を備え、拡張可能なデバッガー データモデルを中心に構築された WinDbg の新しいバージョンです。 WinDbg Preview では、Windows 10 の各バージョンのデバッグがサポートされています。

WinDbg Preview のダウンロード リンクと詳細については、[WinDbg Preview のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools#small-windbg-preview-logo-download-windbg-preview)に関するページを参照してください。

## <a name="standalone-tools-for-debugging-windows-xp-and-windows-vista"></a>Windows XP と Windows Vista のデバッグ用のスタンドアロン ツール

Windows XP、Windows Server 2003、Windows Vista、または Windows Server 2008 をデバッグしている場合 (またはこれらのオペレーティング システムのいずれかを使って Debugging Tools for Windows を実行している場合) は、デバッグ ツールの Windows 7 リリースを使う必要があります。 これは、Windows 7 と .NET Framework 4.0 用 SDK に含まれています。

> [!IMPORTANT]
> SDK for Windows 7 をインストールする際に、新しいバージョンの Visual C++ 2010 再頒布可能パッケージによって問題が発生することがあります。 詳細については、Microsoft サポートの「[Windows SDK Fails to Install with Return Code 5100](https://support.microsoft.com/en-us/help/2717426/windows-sdk-fails-to-install-with-return-code-5100)」 (Windows SDK のインストールがリターン コード 5100 で失敗する) を参照してください。

スタンドアロンの Windows XP 用デバッグ ツールを入手します (最初に Windows 7 SDK:[Microsoft Windows SDK for Windows 7 および .NET Framework 4](https://www.microsoft.com/download/confirmation.aspx?id=8279) をダウンロードします)。

Debugging Tools for Windows をスタンドアロン コンポーネントとしてインストールするには、SDK インストーラーを起動し、インストール ウィザードで **Debugging Tools for Windows** を選択し、他のすべてのコンポーネントを選択解除します。

### <a name="related-downloads"></a>関連するダウンロード
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [Windows HLK、HCK、Logo Kit のダウンロード](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit)
* [Windows 向けデバッグ ツール (WinDbg) のダウンロード](https://developer.microsoft.com/windows/hardware/download-windbg)
* [Windows シンボル パッケージのダウンロード](https://developer.microsoft.com/windows/hardware/download-symbols)
* [WDK Insider Preview のダウンロード](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
