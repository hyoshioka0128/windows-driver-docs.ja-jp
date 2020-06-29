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
ms.openlocfilehash: b3f5d23794fa490bc9ed0428c2b3d9f1f70fcc02
ms.sourcegitcommit: df7d6565a4cd2659c46d5fd83ef04a1672c60dbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382733"
---
# <a name="download-the-windows-driver-kit-wdk"></a>Windows Driver Kit (WDK) のダウンロード

WDK は、Windows ドライバーの開発、テスト、展開に使用します。

* [ドライバー開発の新着情報を見る](what-s-new-in-driver-development.md)
* [既知の問題を確認する](https://go.microsoft.com/fwlink/?linkid=872986)

[Windows Insider Program に参加](https://insider.windows.com/)して [WDK Insider Preview ビルド](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewWDK)を入手してください。 Windows Insider Preview ビルドのインストール手順については、「[プレビュー バージョンの Windows Driver Kit (WDK) のインストール](installing-preview-versions-wdk.md)」をご覧ください。

## <a name="wdk-for-windows-10-version-2004"></a>WDK for Windows 10 バージョン 2004

### <a name="download-icon-step-1-install-visual-studio-2019"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2019 をインストールする

WDK には Visual Studio が必要です。 Visual Studio のシステム要件について詳しくは、[Visual Studio 2019 のシステム要件](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)に関する記事をご覧ください。 

このリリースのドライバー開発は、Visual Studio 2019 の次のエディションでサポートされています。

* [Visual Studio Community 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [Visual Studio Professional 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [Visual Studio Enterprise 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

Visual Studio 2019 のインストール時に、 **[C++ によるデスクトップ開発]** ワークロードを選択します。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 WDK for Windows 10 バージョン 2004 と互換性のある SDK のバージョンは、既定の SDK でない可能性があることに注意してください。 正しい SDK を選択するには:

**Visual Studio インストーラー**の **[個別のコンポーネント]** タブで、Windows 10 SDK (10.0.19041.0) を検索し、そのバージョンを選択してからインストールします。 

既に Visual Studio 2019 がインストールされている場合は、Visual Studio のインストールで **[変更]** ボタンを使用して **Windows 10 SDK (10.0.19041.1)** をインストールできます。

WDK では Spectre 軽減策が既定で有効になっていますが、開発対象のアーキテクチャごとに Visual Studio を使用して Spectre 軽減ライブラリをインストールする必要があります。 さらに、ARM または ARM64 用のドライバーを開発するには、Visual Studio を使用してそれらのアーキテクチャ用のビルド ツールもインストールする必要があります。 これらの項目を特定するには、システムにインストールされている最新バージョンの MSVC を把握しておく必要があります。

ご自分のシステムにインストールされている MSVC の最新バージョンを確認するには、**Visual Studio インストーラー**で、 **[インストールの詳細]** の右側のペインにある**ワークロード ページ**に移動して、 **[C++ によるデスクトップ開発]** を展開し、**MSVC v142 - VS 2019 C++ x64/x86 ビルド ツール (V14.xx)** を見つけます (注: **xx** は利用可能な最新のバージョン)。 

この情報 (v14.xx) をメモして **[個別のコンポーネント]** に移動し、**v14.xx** を検索します。 これにより、Spectre 軽減ライブラリを含む、すべてのアーキテクチャのツール セットが返されます。 開発対象のドライバー アーキテクチャを選択します。 

たとえば、v14.25 を検索すると、以下が返されます。

```
MSVC v142 - VS 2019 C++ ARM build tools (v14.25)
MSVC v142 - VS 2019 C++ ARM Spectre-mitigated libs (v14.25)
MSVC v142 - VS 2019 C++ ARM64 build tools (v14.25)
MSVC v142 - VS 2019 C++ ARM64 Spectre-mitigated libs (v14.25)
MSVC v142 - VS 2019 C++ x64/x86 build tools (v14.25)
MSVC v142 - VS 2019 C++ x64/x86 Spectre-mitigated libs (v14.25)
```

### <a name="download-icon-step-2-install-wdk-for-windows-10-version-2004"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 バージョン 2004 のインストール

* [WDK for Windows 10 バージョン 2004 のダウンロード](https://go.microsoft.com/fwlink/?linkid=2128854)

WDK の既定のインストールには、WDK Visual Studio 拡張機能が含まれています。 

## <a name="enterprise-wdk-ewdk-for-windows-10-version-2004"></a>Enterprise WDK (EWDK) for Windows 10 バージョン 2004

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio 2019 Build Tools 16.3.0 と MSVC ツールセット v14.23 が含まれています。  まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。

EWDK では、.NET Framework バージョン 4.7.2 も必要です。 .NET Framework のその他の要件の詳細については、「[.NET Framework のシステム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)」を参照してください。

### <a name="download-icon-ewdk-with-visual-studio-build-tools"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools

* [EWDK for Windows 10 バージョン 2004 のダウンロード](https://docs.microsoft.com/legal/windows/hardware/enterprise-wdk-license-2019)

## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-runtime-requirements"></a>リリース ノートと実行時の要件

Windows 7 以降で Windows 10 バージョン 2004 WDK を実行し、それを使用してこれらのオペレーティング システムのドライバーを開発することができます。

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

* [WDK Insider Preview のダウンロード](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewWDK)
* [以前のバージョンの WDK のダウンロード](other-wdk-downloads.md)
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)
* [Windows HLK のダウンロード](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [Windows デバッグ ツール (WinDbg) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)
* [Windows シンボル パッケージのダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)
