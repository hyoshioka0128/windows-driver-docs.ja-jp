---
title: プレビュー バージョンの Windows Driver Kit (WDK) のインストール
description: 最新のプレリリース バージョンの Windows Driver Kit (WDK) のインストール方法です
keywords:
- Windows Driver Kit (WDK)
- WDK
- Insider Preview
- ダウンロード
- ドライバー
ms.author: eliotgra
ms.date: 07/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 305e5ac725f1ca5c11c68d528f8b8c9909fd3c48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518720"
---
# <a name="installing-preview-versions-of-the-windows-driver-kit-wdk"></a>プレビュー バージョンの Windows Driver Kit (WDK) のインストール

このページでは、Insider Preview (プレリリース) バージョンの Windows Driver Kit (WDK) のインストール手順について説明します。 最新のプレリリース バージョンの WDK と EWDK はこちらのリンク [https://www.microsoft.com/software-download/windowsinsiderpreviewWDK](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK) からダウンロードできます。  

最新の**リリース済み**バージョンの WDK については、「[Download the Windows Driver Kit (WDK) (Windows Driver Kit (WDK) のダウンロード)](download-the-wdk.md)」をご覧ください。 以前のバージョンの WDK のダウンロードについては、「[Other WDK downloads (その他の WDK のダウンロード)](other-wdk-downloads.md)」をご覧ください。  

## <a name="install-windows-driver-kit-wdk-insider-preview"></a>Windows Driver Kit (WDK) Insider Preview をインストールする

### <a name="1-install-visual-studio"></a>1. Visual Studio をインストールする

- WDK では、Visual Studio 2017 がサポートされるようになっています。  すべてのエディションがサポートされます。  WDK では、Visual Studio 2015 はサポートされなくなりました。 
- [https://www.visualstudio.com/downloads/](https://www.visualstudio.com/downloads/) からダウンロードします。 
- ワークロードを選択します: C++ による開発。 
- ARM: ARM ドライバーをビルドするには、さらにコンポーネントをインストールする必要があります: [個別のコンポーネント] -> [コンパイラ、ビルド ツール、およびランタイム] -> [ARM 用 Visual Studio C++ コンパイラとライブラリ]。 
- ARM64: 現在サポートされていません。 

### <a name="2-disable-strong-name-validation"></a>2. 厳密な名前の検証を無効にする

現在、WDK の Visual Studio 拡張機能は厳密な名前で署名されていません。 管理者特権のコマンド プロンプトで次のコマンドを実行して、厳密な名前の検証を無効にします。 

```cpp
reg add HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\StrongName\Verification\*,31bf3856ad364e35 /v TestPublicKey /t REG_SZ /d 00240000048000009400000006020000002400005253413100040000010001003f8c902c8fe7ac83af7401b14c1bd103973b26dfafb2b77eda478a2539b979b56ce47f36336741b4ec52bbc51fecd51ba23810cec47070f3e29a2261a2d1d08e4b2b4b457beaa91460055f78cc89f21cd028377af0cc5e6c04699b6856a1e49d5fad3ef16d3c3d6010f40df0a7d6cc2ee11744b5cfb42e0f19a52b8a29dc31b0 /f

reg add HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\StrongName\Verification\*,31bf3856ad364e35 /v TestPublicKey /t REG_SZ /d 00240000048000009400000006020000002400005253413100040000010001003f8c902c8fe7ac83af7401b14c1bd103973b26dfafb2b77eda478a2539b979b56ce47f36336741b4ec52bbc51fecd51ba23810cec47070f3e29a2261a2d1d08e4b2b4b457beaa91460055f78cc89f21cd028377af0cc5e6c04699b6856a1e49d5fad3ef16d3c3d6010f40df0a7d6cc2ee11744b5cfb42e0f19a52b8a29dc31b0 /f 
```

### <a name="3-install-sdk-insider-preview"></a>3.SDK Insider Preview をインストールする 

[SDK Insider Preview を入手する](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

### <a name="4-install-wdk-insider-preview"></a>4。WDK Insider Preview のインストール

[WDK Insider Preview を入手する](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

> [!Note]   
> インストールの間に、Visual Studio インストーラーによる WDK Visual Studio 拡張機能のインストールの状況が表示されます。 

## <a name="install-enterprise-wdk-ewdk-insider-preview"></a>Enterprise WDK (EWDK) Insider Preview をインストールする

EWDK は、ドライバーを構築するためのスタンドアロン自己完結型コマンドライン環境です。  Build Tools for Visual Studio 2017、SDK、WDK、および ARM64 ドライバー開発のサポートが含まれています。 詳しくは、[Installing the Enterprise WDK (Enterprise WDK のインストール)](https://docs.microsoft.com/windows-hardware/drivers/develop/installing-the-enterprise-wdk) に関する記事をご覧ください。 

[Enterprise Windows Driver Kit (EWDK) Insider Preview を入手する](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)

最初に、ISO をマウントして、LaunchBuildEnv をクリックします。 

## <a name="run-time-requirements-for-the-wdk-and-the-ewdk"></a>WDK と EWDK の実行時の要件

WDK には Visual Studio が必要です。 Visual Studio のシステム要件について詳しくは、「[Visual Studio 2017 製品ファミリのシステム要件](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)」をご覧ください。

さらに、EWDK には .NET 4.6.1 が必要です。 .NET の動作環境について詳しくは、「[.NET Framework のシステム要件](https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs)」をご覧ください。

WDK Insider Preview と EWDK Insider Preview を使用すると、次のオペレーティング システムで動作するドライバーを開発できます。 

|クライアントの OS|サーバー OS|
|---|---|
|Windows 10|Windows Server 2016|
|Windows 8.1|Windows Server 2012 R2|
|Windows 8|Windows Server 2012|
|Windows 7|Windows Server 2008 R2 SP1|

