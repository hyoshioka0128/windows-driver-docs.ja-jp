---
title: Windows Driver Kit (WDK) のダウンロード
description: 最新リリース版の Windows Driver Kit (WDK) のダウンロード方法
ms.assetid: 7b5e253b-3bcd-41e3-a646-0f95ce416f87
keywords:
- Windows Driver Kit (WDK)
- WDK
- ダウンロード
- ドライバー
ms.date: 03/16/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fb64e0e87ad62c4da101f066378d17f48002a2ca
ms.sourcegitcommit: 3794904c6f741bdc407dfe22341080646602f972
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80807615"
---
# <a name="download-the-windows-driver-kit-wdk"></a>Windows Driver Kit (WDK) のダウンロード

WDK は、Windows ドライバーの開発、テスト、展開に使用します。

* [ドライバー開発の新着情報を見る](what-s-new-in-driver-development.md)
* [既知の問題を確認する](https://go.microsoft.com/fwlink/?linkid=872986)

Windows Insider Program に参加して [WDK Insider Preview ビルド](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)を入手してください。 Windows Insider Preview ビルドのインストール手順については、「[プレビュー バージョンの Windows Driver Kit (WDK) のインストール](installing-preview-versions-wdk.md)」をご覧ください。

## <a name="wdk-for-windows-10-version-1903"></a>WDK for Windows 10 Version 1903

### <a name="download-icon-step-1-install-visual-studio-2019"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2019 をインストールする

WDK には Visual Studio が必要です。 Visual Studio のシステム要件について詳しくは、[Visual Studio 2019 のシステム要件](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)に関する記事をご覧ください。 

このリリースのドライバー開発は、Visual Studio 2019 の次のエディションでサポートされています。

* [Visual Studio Community 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [Visual Studio Professional 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [Visual Studio Enterprise 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

Visual Studio 2019 のインストール時に、 **[C++ によるデスクトップ開発]** ワークロードを選択します。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 WDK for Windows 10 バージョン 1903 と互換性のある SDK のバージョンは、既定の SDK でない可能性があることに注意してください。 正しい SDK を選択するには:

1. **Visual Studio インストーラー**の **[ワークロード]** タブの **[インストールの詳細]** で、 **[ユニバーサル Windows プラットフォーム開発]** を展開します。
1. **[オプション]** で **[Windows 10 SDK (10.0.18362.0)]** を選択します。
1. インストールを続行します。

既に Visual Studio 2019 がインストールされている場合は、Visual Studio のインストールで **[変更]** ボタンを使用して Windows 10 SDK (10.0.18362.0) をインストールできます。

x86/x64 用の MSVC v142 ビルド ツールの正しいバージョンがインストールされていることを確認するには、以下の手順に従ってください。 
1. **[個別のコンポーネント]** を選択します。
1. **[コンパイラ、ビルド ツール、およびランタイム]** で、オプション **[MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (v14.21)]** ボックスがオンになっていることを確認し、オンになっていない場合はオンにしてください。
1. より新しいバージョンの MSVC ビルド ツールが既にインストールされている場合、VS 内のプロジェクトのプロパティで、MSVC バージョンを設定する必要があります。 **[構成プロパティ]** 、 **[詳細]** に移動し、 **[MSVC ツールセット バージョン]** を「**14.21.XXXX**」に設定します。 コマンド ラインを使用する場合は、この [VS へのリンク](https://docs.microsoft.com/cpp/build/building-on-the-command-line?view=vs-2019)を参照してください。

ARM/ARM64 ドライバー開発の場合、以下の操作を行います。 

1. **[個別のコンポーネント]** を選択します。 
1. **[コンパイラ、ビルド ツール、およびランタイム]** で、 **[MSVC v142 - VS 2019 C++ ARM ビルド ツール (v14.21)]** と **[MSVC v142 - VS 2019 C++ ARM64 ビルド ツール (v14.21)]** を選択します。

ドライバーをビルドするアーキテクチャごとに、Spectre 軽減ライブラリをインストールする必要があります。 **[個々のコンポーネント]** タブに移動し、見出し **[コンパイラ、ビルド ツール、およびランタイム]** で、以下を実行します。
  * x86 と x64 の場合は、 **[MSVC v142 - VS 2019 C++ x64/x86 Spectre 軽減ライブラリ (v14.21)]** を選択します。
  * ARM の場合は、 **[MSVC v142 - VS 2019 C++ ARM Spectre 軽減ライブラリ (v14.21)]** を選択します。
  * ARM64 の場合は、 **[MSVC v142 - VS 2019 C++ ARM64 Spectre 軽減ライブラリ (v14.21)]** を選択します。

### <a name="download-icon-step-2-install-wdk-for-windows-10-version-1903"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 Version 1903 のインストール

* [WDK for Windows 10 Version 1903 のダウンロード](https://go.microsoft.com/fwlink/?linkid=2085767)

WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 

## <a name="enterprise-wdk-ewdk-for-windows-10-version-1903"></a>Enterprise WDK (EWDK) for Windows 10 バージョン 1903

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio 2019 Build Tools 16.0.0 が含まれています。  まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。

EWDK では、.NET Framework バージョン 4.7.2 も必要です。 .NET Framework のその他の要件の詳細については、「[.NET Framework のシステム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)」を参照してください。

### <a name="download-icon-ewdk-with-visual-studio-build-tools"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools

* [EWDK for Windows 10 Version 1903 のダウンロード](https://docs.microsoft.com/legal/windows/hardware/enterprise-wdk-license-2019)

## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-runtime-requirements"></a>リリース ノートと実行時の要件

WDK を使うと、次のオペレーティング システムで動作するドライバーを開発できます。

|クライアントの OS|サーバーの OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

### <a name="universal-windows-driver-samples"></a>ユニバーサル Windows ドライバーのサンプル

ユニバーサル Windows ドライバーのサンプルをダウンロードするには、次のいずれかを実行します。

* [GitHub](https://github.com/Microsoft/Windows-driver-samples) のドライバー サンプル ページにアクセスし、 **[クローンまたはダウンロード]** をクリックしてから **[ZIP をダウンロード]** をクリックします。
* [GitHub Extension for Visual Studio](https://visualstudio.github.com/) をダウンロードしてから、GitHub リポジトリに接続します。
* [Microsoft サンプル ポータル](https://docs.microsoft.com/samples/browse/?products=windows-wdk)上でドライバーのサンプルを参照します。

## <a name="related-downloads"></a>関連するダウンロード

* [WDK Insider Preview のダウンロード](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [以前のバージョンの WDK のダウンロード](other-wdk-downloads.md)
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)
* [Windows HLK のダウンロード](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [Windows デバッグ ツール (WinDbg) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)
* [Windows シンボル パッケージのダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)
