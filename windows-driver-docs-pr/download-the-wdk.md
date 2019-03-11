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
ms.openlocfilehash: ec30a1b0ac4711f6170c1bf30fa1f0a9e9d0d1e4
ms.sourcegitcommit: 20109e8686f33fd3d683fc1c253b17bfeac0e0c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2019
ms.locfileid: "56519008"
---
# <a name="download-the-windows-driver-kit-wdk"></a>Windows Driver Kit (WDK) のダウンロード

WDK は、Windows ドライバーの開発、テスト、展開に使用します。 WDK の最新の公開バージョンは、以下で入手できます。 

Windows Insider Program に参加して [WDK Insider Preview ビルド](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)を入手してください。 Windows Insider Preview ビルドのインストール手順については、「[プレビュー バージョンの Windows Driver Kit (WDK) のインストール](installing-preview-versions-wdk.md)」をご覧ください。

* [ドライバー開発の新着情報を見る](what-s-new-in-driver-development.md) 
* [既知の問題を確認する](https://go.microsoft.com/fwlink/?linkid=872986)

## <a name="wdk-for-windows-10-version-1809"></a>WDK for Windows 10 Version 1809

### <a name="download-iconimagesdownload-installpng-step-1-install-visual-studio-2017"></a>![ダウンロード アイコン](images/download-install.png) 手順 1:Visual Studio 2017 のインストール 
Visual Studio 2017 の次のエディションでドライバー開発がサポートされています。 

* [Visual Studio Community 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)
* [Visual Studio Professional 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15) 
* [Visual Studio Enterprise 2017 のダウンロード](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15)

Visual Studio のインストール時に、**[C++ によるデスクトップ開発]** ワークロードを選びます。 Windows 10 ソフトウェア開発キット (SDK) が自動的に含められ、右側の **[概要]** ウィンドウに表示されます。 

ARM/ARM64 ドライバーを開発するには、**[個別のコンポーネント]** を選び、**[コンパイラ、ビルド ツール、およびランタイム]** の下で **[ARM 用 Visual Studio C++ コンパイラとライブラリ] または [ARM 64用 Visual Studio C++ コンパイラとライブラリ]** を選びます。


### <a name="download-iconimagesdownload-installpng-step-2-install-wdk-for-windows-10-version-1809"></a>![ダウンロード アイコン](images/download-install.png) 手順 2:WDK for Windows 10 Version 1809 のインストール

* [WDK for Windows 10 Version 1809 のダウンロード](https://go.microsoft.com/fwlink/?linkid=2026156) 

1709 リリースの新機能:WDK をインストールすると、既定で、WDK Visual Studio 拡張機能がインストールされます。 WDK VS 統合が機能するためには、この拡張機能をインストールする必要があります。 

## <a name="enterprise-wdk-for-windows-10-version-1809-ewdk"></a>Enterprise WDK for Windows 10 Version 1809 (EWDK) 

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。 これには、Visual Studio Build Tools、SDK、WDK が含まれています。  EWDK の最新の公開バージョンには、Visual Studio Build Tools 15.8.9 が含まれています。  まず、ISO をマウントし、**LaunchBuildEnv** を実行してください。 

### <a name="download-iconimagesdownload-installpng-ewdk-with-visual-studio-build-tools"></a>![ダウンロード アイコン](images/download-install.png) EWDK with Visual Studio Build Tools

* [EWDK for Windows 10 Version 1809 のダウンロード](https://developer.microsoft.com/windows/hardware/license-terms-EWDK)


## <a name="additional-information"></a>追加情報

### <a name="release-notes-and-run-time-requirements"></a>リリース ノートと実行時の要件

WDK には Visual Studio が必要です。Visual Studio に関するシステム要件について詳しくは、[Visual Studio 2017 のシステム要件](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)に関する記事をご覧ください。 

EWDK では、さらに .NET 4.6.1 も必要になります .NET を実行するための要件について詳しくは、[.NET Framework のシステム要件](https://docs.microsoft.com/dotnet/framework/get-started/system-requirements)に関する記事をご覧ください。 

WDK を使うと、次のオペレーティング システムで動作するドライバーを開発できます。 

|クライアントの OS|サーバー OS|
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

