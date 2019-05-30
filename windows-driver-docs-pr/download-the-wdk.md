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
ms.openlocfilehash: 92dfee5d72fee1bc49c97ba99b7a5182d1a9201a
ms.sourcegitcommit: a0da18a4c5c636c4980e8ed77c6879e617299580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66373154"
---
# <a name="download-the-windows-driver-kit-wdk"></a>Windows Driver Kit (WDK) のダウンロード

WDK は、Windows ドライバーの開発、テスト、展開に使用します。 WDK の最新の公開バージョンは、以下で入手できます。

Windows Insider Program に参加して [WDK Insider Preview ビルド](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)を入手してください。 Windows Insider Preview ビルドのインストール手順については、「[プレビュー バージョンの Windows Driver Kit (WDK) のインストール](installing-preview-versions-wdk.md)」をご覧ください。

* [ドライバー開発の新着情報を見る](what-s-new-in-driver-development.md)
* [既知の問題を確認する](https://go.microsoft.com/fwlink/?linkid=872986)

## <a name="wdk-for-windows-10-version-1903"></a>WDK の Windows 10、バージョンが 1903

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2019"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2019 をインストールします。

Visual Studio 2019 の次のエディションでは、ドライバーの開発をサポートします。

* [Visual Studio Community 2019 をダウンロードします。](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* [Visual Studio Professional 2019 をダウンロードします。](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=16)
* [Visual Studio Enterprise 2019 をダウンロードします。](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=16)

Visual Studio のインストール時に、 **[C++ によるデスクトップ開発]** ワークロードを選びます。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。

ARM/ARM64 ドライバーを開発するには、 **[個別のコンポーネント]** を選び、 **[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選びます。

用のドライバーをビルド、Spectre の軽減ライブラリを通じて個々 のコンポーネント]-> [をインストールする各アーキテクチャのコンパイラ、ビルド ツール、およびランタイム MSVC v142 - VS 2019 C+ x64 または x86 Spectre 軽減 libs (v14.21)]-> [です。 

### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1903"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK の Windows 10、バージョンが 1903 をインストールします。

* [WDK の Windows 10、バージョンが 1903 をダウンロードします。](https://go.microsoft.com/fwlink/?linkid=2085767)

1709 リリースの新機能:WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 WDK VS 統合が機能するためには、この拡張機能をインストールする必要があります。

## <a name="enterprise-wdk-for-windows-10-version-1903-ewdk"></a>エンタープライズ WDK for Windows 10 バージョン 1903 (EWDK)

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新のパブリック バージョンには、Visual Studio 2019 ビルド ツール 16.0.0 が含まれています。  まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools

* [EWDK for Windows 10 バージョン 1903 をダウンロードします。](https://developer.microsoft.com/windows/hardware/license-terms-EWDK-2)

## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-run-time-requirements"></a>リリース ノートと実行時の要件

WDK の詳細については、Visual Studio のシステム要件を確認してください詳細については、Visual Studio が必要です[Visual Studio 2019 のシステム要件](https://docs.microsoft.com/visualstudio/releases/2019/system-requirements)します。

EWDK さらに必要な .NET 4.7.2、詳細については、どのような .NET 上で実行してくださいレビュー [.NET Framework システム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)します。

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
* [Windows アセスメント & デプロイメント キット (Windows ADK) のダウンロード](https://developer.microsoft.com/windows/hardware/windows-assessment-deployment-kit)
* [Windows HLK、HCK、Logo Kit のダウンロード](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit)
* [Windows 向けデバッグ ツール (WinDbg) のダウンロード](https://developer.microsoft.com/windows/hardware/download-windbg)
* [Windows シンボル パッケージのダウンロード](https://developer.microsoft.com/windows/hardware/download-symbols)
