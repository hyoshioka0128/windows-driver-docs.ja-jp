---
ms.assetid: 9F1E79FF-D38E-484A-8AEB-FC9A105BF709
title: カスタム ドライバー インストール スクリプトを作成する方法
description: テスト コンピューターにドライバー パッケージより多くのパッケージをインストールする必要がある場合は、インストール時にカスタム コマンド スクリプトを実行できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34688d9e3b765f505c0fce0105b2c1d20449a7c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518928"
---
# <a name="how-to-create-a-custom-driver-installation-script"></a>カスタム ドライバー インストール スクリプトを作成する方法

テスト コンピューターへのドライバー パッケージのインストール以外にも必要な処理がある展開シナリオでは、インストール時に独自のカスタム コマンド スクリプトを実行することができます。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   テスト署名され、インストールの準備ができているドライバー パッケージ。 まずドライバーを作ってビルドし、次にインストール用のドライバー パッケージを作る必要があります。 詳しくは、「[ドライバーのビルド](building-a-driver.md)」と「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。
-   展開用に構成され、プロビジョニングされたテスト コンピューター。 「[Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)」をご覧ください。

<a name="instructions"></a>手順
------------

### <a name="span-idtorunyourowncustomcommandscriptsuponinstallationspanspan-idtorunyourowncustomcommandscriptsuponinstallationspanspan-idtorunyourowncustomcommandscriptsuponinstallationspanstep-1-to-run-your-own-custom-command-scripts-upon-installation"></a><span id="To_run_your_own_custom_command_scripts_upon_installation"></span><span id="to_run_your_own_custom_command_scripts_upon_installation"></span><span id="TO_RUN_YOUR_OWN_CUSTOM_COMMAND_SCRIPTS_UPON_INSTALLATION"></span>ステップ 1:インストール時に独自のカスタム コマンド スクリプトを実行するには

ドライバー パッケージのプロジェクト プロパティ ページで、テスト コンピューターにドライバー パッケージを自動的に展開するかどうかを構成できます。 これらのページからカスタム インストール スクリプトを実行することもできます。 各構成でドライバー ソリューションをビルドするたびに、自動的にドライバーが展開されるようにすることができます。 展開について詳しくは、「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」と「[ドライバー プロジェクトの展開プロパティ](deployment-properties-for-driver-projects.md)」をご覧ください。

1.  ドライバー パッケージ プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。

2.  ドライバー パッケージのプロパティ ページで、**[構成プロパティ]**、**[Driver Settings] (ドライバーの設定)**、**[Deployment]** (配置) の順にクリックします。

3.  **[配置を有効にする]** をクリックし、使用するテスト コンピューターを選びます。

4.  **[Custom Command Line]** (カスタム コマンド ライン) をクリックします。 ボックス内で、インストール時に実行するカスタム コマンド スクリプトを入力します。

5.  **[Additional Files]** (追加ファイル) ボックスで、テスト コンピューターにコピーするコマンド スクリプトとその他のインストール ファイルを追加します。 ドライバーが展開されると、追加のファイルはリモート コンピューターの *%Systemdrive%*\\drivertest\\drivers フォルダーにコピーされます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [ドライバー プロジェクトの展開プロパティ](deployment-properties-for-driver-projects.md)
* [Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)
* [ドライバーのビルド](building-a-driver.md)
* [ドライバー パッケージの作成](creating-a-driver-package.md)
 

 






