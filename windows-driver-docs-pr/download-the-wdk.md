---
title: Windows Driver Kit (WDK) のダウンロード
description: 最新リリース版の Windows Driver Kit (WDK) のダウンロード方法
ms.assetid: 7b5e253b-3bcd-41e3-a646-0f95ce416f87
keywords:
- Windows Driver Kit (WDK)
- WDK
- ダウンロード
- ドライバー
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9b5474cc1f29ed61568ff616ca941252008da284
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372010"
---
# <a name="download-the-windows-driver-kit-wdk"></a>Windows Driver Kit (WDK) のダウンロード

WDK は、Windows ドライバーの開発、テスト、展開に使用します。 WDK の最新の公開バージョンは、以下で入手できます。

Windows Insider Program に参加して [WDK Insider Preview ビルド](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)を入手してください。 Windows Insider Preview ビルドのインストール手順については、「[プレビュー バージョンの Windows Driver Kit (WDK) のインストール](installing-preview-versions-wdk.md)」をご覧ください。

* [ドライバー開発の新着情報を見る](what-s-new-in-driver-development.md)
* [既知の問題を確認する](https://go.microsoft.com/fwlink/?linkid=872986)

## <a name="wdk-for-windows-10-version-1903"></a>WDK for Windows 10 Version 1903

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2019"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2019 をインストールする

Visual Studio 2019 の次のエディションでドライバー開発がサポートされています。

* [Visual Studio Community 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [Visual Studio Professional 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [Visual Studio Enterprise 2019 のダウンロード](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

Visual Studio 2019 のインストール時に、 **[C++ によるデスクトップ開発]** ワークロードを選択します。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 ただし、WDK for Windows 10 Version 1903 と互換性のある SDK のバージョンは、現在、既定の SDK ではありません。 正しい SDK を選択するには:

* **Visual Studio インストーラー**の **[ワークロード]** タブの **[インストールの詳細]** で、 **[ユニバーサル Windows プラットフォーム開発]** を展開します。
* **[オプション]** で **[Windows 10 Preview SDK (10.0.18362.0) ]** を選択します。
* インストールを続行します。

既に Visual Studio 2019 がインストールされている場合は、Visual Studio のインストールで **[変更]** ボタンを使用して Windows 10 Preview SDK (10.0.18362.0) をインストールできます。

ARM/ARM64 ドライバーを開発するには、 **[個別のコンポーネント]** を選び、 **[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選びます。

ドライバーを構築するアーキテクチャごとに、[個別のコンポーネント] -> [コンパイラ、ビルド ツール、およびランタイム] -> MSVC v142 - VS 2019 C+ x64/x86 Spectre-mitigated のスペクター軽減ライブラリ (v14.21) を介して、スペクター軽減ライブラリをインストールします。

### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1903"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 Version 1903 のインストール

* [WDK for Windows 10 Version 1903 のダウンロード](https://go.microsoft.com/fwlink/?linkid=2085767)

1709 リリースの新機能:WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 WDK VS 統合が機能するためには、この拡張機能をインストールする必要があります。

## <a name="enterprise-wdk-for-windows-10-version-1903-ewdk"></a>Enterprise WDK for Windows 10 Version 1903 (EWDK)

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio 2019 Build Tools 16.0.0 が含まれています。  まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools

* [EWDK for Windows 10 Version 1903 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-EWDK-2)

## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-run-time-requirements"></a>リリース ノートと実行時の要件

WDK には Visual Studio が必要です。Visual Studio に関するシステム要件の詳細については、[Visual Studio 2019 のシステム要件](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)に関する記事を参照してください。

EWDK では、さらに .NET 4.7.2 も必要になります .NET を実行するための要件の詳細については、[.NET Framework のシステム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)に関する記事を参照してください。

WDK を使うと、次のオペレーティング システムで動作するドライバーを開発できます。

|クライアントの OS|サーバーの OS|
|-|-|
|Windows 10|Windows Server 2019、Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
Windows 8|Windows Server 2012|
Windows 7|Windows Server 2008 R2 SP1|

### <a name="universal-windows-driver-samples"></a>ユニバーサル Windows ドライバーのサンプル

ユニバーサル Windows ドライバーのサンプルを入手するには、次のいずれかを実行します。

* [GitHub](https://github.com/Microsoft/Windows-driver-samples) のドライバー サンプル ページにアクセスし、ページの右側にある **[Clone or download] (クローンまたはダウンロード) > [Download ZIP] (ZIP をダウンロード)** をクリックします。
* [GitHub Extension for Visual Studio](https://visualstudio.github.com/) をダウンロードして、GitHub リポジトリに接続します。
* [ドライバー サンプルの最新情報をご覧ください](https://developer.microsoft.com/windows/hardware/drivers-code-samples)。

## <a name="related-downloads"></a>関連するダウンロード

* [WDK Insider Preview のダウンロード](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
* [以前のバージョンの WDK のダウンロード](other-wdk-downloads.md)
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://docs.microsoft.com/windows-hardware/get-started/adk-install)
* [Windows HLK、HCK、Logo Kit のダウンロード](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)
* [Windows 向けデバッグ ツール (WinDbg) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)
* [Windows シンボル パッケージのダウンロード](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols)
