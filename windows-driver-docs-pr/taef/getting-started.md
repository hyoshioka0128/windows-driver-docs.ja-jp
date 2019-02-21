---
title: TAEF の概要
description: テストの作成と実行フレームワーク (TAEF) の概要
ms.assetid: 7F57C5EF-141A-4303-9B9F-2EC118324BF8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc47b4b8e3dcf60c8fefdbbb55cf08f98cbb1a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538190"
---
# <a name="getting-started"></a>作業の開始


## <a name="installation"></a>インストール


インストールするときに、 [Windows Driver Kit](https://developer.microsoft.com/windows/hardware/windows-driver-kit)、TAEF ファイルは、テスト中、\\ランタイム\\WDK の TAEF サブディレクトリ。 設定すると展開については、テスト コンピューターをセットアップする手順に従ってください[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)または[ドライバーの展開用にプロビジョニングして、(WDK 8)のテスト](https://msdn.microsoft.com/library/windows/hardware/hh698272)、TAEF ファイルは、テスト コンピューターにインストールされています。

TAEF ファイルを手動でインストールすることも参照してください[手動でインストールして、テスト コンピューターで TAEF をアンインストール](#manually-installing-and-uninstalling-taef-on-a-test-computer)します。

## <a name="authoring-tests"></a>テストの作成


TAEF では、ネイティブまたはマネージの関係を持つユーザーは制限されません。 ユーザーは、テストを作成する際に最も生産性の高い言語を選択できます。 TAEF は、C および C++ でのテストの記述をサポートしているC#、JScript および VBScript です。

詳細については、次を参照してください。[オーサリング テスト](authoring-tests.md)します。

## <a name="executing-tests"></a>テストの実行


テストの実行は、"TE.exe"ツールをコマンド プロンプトでのテスト ファイルを渡す場合だけです。 たとえば、次を実行します。

``` syntax
TE.exe UnitTests\Wex.Common.Tests.dll
```

詳細については、次を参照してください。[テストの実行](executing-tests.md)します。

## <a name="manually-installing-and-uninstalling-taef-on-a-test-computer"></a>手動でインストールして、テスト コンピューターでの TAEF のアンインストール


WDK と Visual Studio を使用せず、コンピューターでテストを実行する場合は、次の手順を実行。

**TAEF を手動でインストールするには**

1.  Visual Studio と WDK を開発用のコンピューターにインストールします。
2.  テスト コンピューターに、WDK をインストールしたコンピューターから、すべて TAEF のインストール ファイルをコピーします。 TAEF インストール ファイル (\*.msi と\*.cab ファイル) は、%programfiles% に\\Windows キット\\8.0\\テスト\\開発システム上のランタイムのディレクトリ。
3.  テスト コンピューターでは、コマンド プロンプト ウィンドウを開き、コピーした TAEF インストール ファイルを含むディレクトリに移動します。 TAEF をインストールするには、次のコマンドを実行します。 実行、 \*.msi テスト コンピューターのアーキテクチャに一致します。

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x64-x64_en-us.msi"
    ```

    - または -

    ``` syntax
    msiexec /i "Test Authoring and Execution Framework x86-x86_en-us.msi"
    ```

    これを TAEF ファイルがインストールされます\\Program Files\\Windows キット\\8.0\\テスト\\ランタイム\\TAEF\\テスト システムにします。

**TAEF を手動でアンインストールするには**

1.  Te.Service を停止します。 Microsoft 管理コンソール (compmgmt.msc) を開きます。 サービスとアプリケーションに移動\\サービスを探し、Te.Service です。 Te.Service を右クリックし、をクリックして**停止**します。
2.  コントロール パネルに移動して\\プログラム\\プログラムと機能をアンインストールし、**テストの作成と実行フレームワーク プログラム**します。

 

 





