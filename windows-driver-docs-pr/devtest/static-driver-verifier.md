---
title: 静的ドライバー検証ツール
description: 静的ドライバー検証ツール
ms.assetid: 74feeb16-387c-4796-987a-aff3fb79b556
keywords:
- ドライバー WDK、Static Driver Verifier の確認
- ドライバーの検証 WDK、Static Driver Verifier
- Static Driver Verifier WDK
- StaticDV WDK
- SDV WDK
- WDK の SDV のパス
- WDK のコンパイル時の静的検証ツール
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0b1dd0732b11b435d4956ffca95b1be938482fbe
ms.sourcegitcommit: f520be298d14434610dd8b824adc81218ea68e58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141832"
---
# <a name="static-driver-verifier"></a>静的ドライバー検証ツール

Static Driver Verifier ("StaticDV"または"SDV"とも呼ばれます) は、Windows カーネル モード ドライバーのソース コードを体系的に分析する静的検証ツールです。 SDV は、欠陥およびドライバー設計の問題を検出できるコンパイル時ツールです。 一連のインターフェイスの規則とオペレーティング システムのモデルに基づいて、SDV は、Windows オペレーティング システムのカーネルのドライバーが正しく対話するかどうかを決定します。

## <a name="installing-static-driver-verifier"></a>Static Driver Verifier をインストールします。

Static Driver Verifier はの一部、 [Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)両方完全 WDK エクスペリエンスでは、スタンドアロンのエンタープライズ WDK でし。  さらに、ビジュアルC++for Visual Studio の再頒布可能パッケージは、SDV を実行するために必要な。 次を参照してください。

* [Visual Studio 2019 再配布](https://docs.microsoft.com/visualstudio/releases/2019/redistribution)
* [Visual C++ for Visual Studio 2017 再頒布可能パッケージ](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
* [Visual C++ for Visual Studio 2013 の再頒布可能パッケージ](https://www.microsoft.com/download/details.aspx?id=40784)  

バージョンの SDV は、WDK for Windows 10、1809 以前のバージョンで使用できる、 [for Visual Studio 2012 の Visual C 再頒布可能パッケージ](https://my.visualstudio.com/Downloads?pid=1452)2017 パッケージではなくインストールする必要があります。

## <a name="visual-studio-integration"></a>Visual Studio の統合

Static Driver Verifier は、Visual Studio に統合されます。 Visual Studio ドライバーのプロジェクトでは、静的分析を実行できます。 起動、構成、およびから Static Driver Verifier の制御、**ドライバー** Visual Studio のメニュー。

## <a name="static-driver-verifier-documentation"></a>Static Driver Verifier のドキュメント

* [Static Driver Verifier の既知の問題](https://docs.microsoft.com/windows-hardware/drivers/develop/static-driver-verifier-known-issues):Static Driver Verifier の最新の既知の問題を一覧表示します。
* [Static Driver Verifier を使用してドライバーで障害が検出する](using-static-driver-verifier-to-find-defects-in-drivers.md):Visual Studio 環境でドライバー コードの分析を開始する必要がありますがわかります。
* [Static Driver Verifier のコマンド (MSBuild)](-static-driver-verifier-commands--msbuild-.md):Visual Studio コマンド プロンプト ウィンドウでの SDV の実行に使用する MSBuild コマンドが表示されます。
* [Static Driver Verifier の紹介](introducing-static-driver-verifier.md):静的分析ツールの概要を示します。
* [Static Driver Verifier を使用する](using-static-driver-verifier.md):使用して、静的分析ツールの構成についてを説明します。
* [Static Driver Verifier レポート](static-driver-verifier-report.md):静的コード分析の詳細なトレースを表示するビューアーについて説明します。
* [Static Driver Verifier ルール](static-driver-verifier-rules.md):ルールは、ドライバー モデルと、オペレーティング システムのカーネル インターフェイスの適切な相互作用するための要件を定義します。
* [Static Driver Verifier 参照](static-driver-verifier-reference.md):関数のロールの種類、SDV 構成ファイル、エラー、および警告メッセージに関する参照情報を提供します。

## <a name="finding-bugs-in-windows-driver-code"></a>Windows ドライバー コードのバグの検索

マイクロソフトは、wdk サンプル ドライバーをテストして、Microsoft Windows オペレーティング システムに含まれるカーネル モード ドライバーをテストする SDV を使用します。 SDV は DDI 準拠規則の特定のドライバー モデルを使用して、適切なドライバーの動作を確認できます。 たとえば、SDV を確認できるドライバー。

* 適切な IRQL で関数を呼び出す
* 取得し、正しい順序でロックを解放します。
* 不適切に使用される I/O 要求パケット (IRP) を処理する関数

SDV は、すべての可能なドライバーのコード パスを検証します。 徹底的なテストにも可能性があるないあいまいなパスで重大なエラーを見つけるために設計されています。

## <a name="additional-resources"></a>その他の資料

SDV を検証するドライバーの詳細については、次を参照してください[ドライバーのサポート。](supported-drivers.md)

詳細および Static Driver Verifier の使用に関するヒントについては、次を参照してください。

* [Windows ハードウェア認定のブログ](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)
* [Windows カーネルのコミュニティ サイト](https://techcommunity.microsoft.com/t5/Windows-Kernel/ct-p/WindowsKernel)
* [Windows ハードウェア テストおよび認定フォーラム](https://social.msdn.microsoft.com/Forums/home?forum=whck)
