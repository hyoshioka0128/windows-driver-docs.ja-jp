---
ms.assetid: 6e8be17d-6e98-441e-9a2c-e62a007786ee
title: ドライバーの開発、テスト、および展開
description: Windows Driver Kit (WDK) 8 以降、Windows ドライバーの開発環境とデバッガーは Microsoft Visual Studio に統合されています。
keywords:
- ドライバーの開発
- ドライバーのデバッグ
- ドライバーのテスト
- ドライバーの展開
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: b89f67ab77281bd37d424dbb2bca5cfb7f8b2c03
ms.sourcegitcommit: 276a3aef2d4463bbe653d30ed55d7bab20000aa6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65814906"
---
# <a name="developing-testing-and-deploying-drivers"></a>ドライバーの開発、テスト、および展開

Windows のドライバー開発環境と Windows デバッガーは、Microsoft Visual Studio に統合されています。 この統合されたドライバー開発環境では、ドライバーのコーディング、ビルド、パッケージ化、展開、デバッグ、テストに必要なツールのほとんどが Visual Studio のユーザー インターフェイスに用意されています。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/9673727b-89ef-4a54-8228-dad41dbd8201]

統合開発環境をセットアップするには、まず Visual Studio をインストールしてから WDK をインストールします。 Visual Studio と WDK の入手方法について詳しくは、[こちら](https://go.microsoft.com/fwlink/p/?linkid=239721)をご覧ください。 [Debugging Tools for Windows](https://msdn.microsoft.com/Library/Windows/Hardware/Ff551063) は、WDK のインストールに含まれています。

WDK は MSBuild.exe を使用します。これは、Visual Studio のユーザー インターフェイスとコマンド ラインツールの両方で使用できます。 Visual Studio の環境で作成されたドライバーは、Project ファイルと Solution ファイルを使って、プロジェクトまたはプロジェクトのグループを記述します。 Visual Studio 環境には、レガシの Sources ファイルと Dirs ファイルを Project ファイルと Solution ファイルに変換するツールが用意されています。

Visual Studio 開発環境には、次のテンプレートが用意されています。

-   新しいドライバー
-   ドライバー パッケージ
-   新しいテスト
-   既存のテストの拡張
-   カスタム ドライバーの展開スクリプト

Visual Studio 環境では、ビルド プロセスが自動的にドライバー パッケージを作成して署名するように、ビルド プロセスを構成することができます。 Visual Studio で静的分析ツールと実行時分析ツールを利用できます。 ドライバーが再ビルドされるたびに、自動的にドライバーがテスト用のターゲット コンピューターに展開されるように、ターゲット コンピューターを構成できます。 Visual Studio で、ターゲット コンピューターに対してカーネル モード デバッグ セッションを確立できます。 豊富な実行時テストのセットから選択することも、独自のテストを作成することもできます。

このセクションのトピックでは、ドライバーの開発、展開、テストに含まれるさまざまなタスクを Visual Studio を使って実行する方法を示します。

## <a name="additional-videos"></a>追加のビデオ

上記のビデオに加えて、Windows ドライバー ドキュメントの次のページにビデオがあります。

* [ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/develop/debugging-a-driver)
* [HID の新機能](https://docs.microsoft.com/windows-hardware/drivers/hid/what-s-new-in-hid)
* [Microsoft Message Analyzer を使用して USB トレースをキャプチャして表示する](https://docs.microsoft.com/windows-hardware/drivers/usbcon/capture-and-view-ing-usb-traces-with-microsoft-message-analyzer-)
* [WDF での Windows Performance Toolkit (WPT) の使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-windows-performance-toolkit--wpt--with-wdf)
* [ビデオ:デバッガーなしでドライバー IFR ログにアクセスする](https://docs.microsoft.com/windows-hardware/drivers/wdf/video--accessing-driver-ifr-logs-without-a-debugger)
* [ビデオ:WDF ソース コードでのドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/video--debugging-your-driver-with-wdf-source-code)
* [ビデオ:UMDF ドライバーのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/wdf/videos--debugging-umdf-drivers)


