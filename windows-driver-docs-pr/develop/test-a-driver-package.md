---
ms.assetid: 5BA0A193-1147-4BAD-A6CA-453856E621A2
title: ドライバー パッケージをテストする方法
description: Visual Studio を使ってドライバー パッケージをテスト コンピューターに展開およびインストールし、その後、ドライバーがインストールされて動作していることを検証できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfa6656c71d46ada73349f3cf0f5c56d30a425b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518771"
---
# <a name="how-to-test-a-driver-package"></a>ドライバー パッケージをテストする方法

Visual Studio を使ってドライバー パッケージをテスト コンピューターに展開およびインストールし、その後、ドライバーがインストールされて動作していることを検証できます。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   インストールの準備ができているドライバー パッケージ。 まずドライバーを作ってビルドし、次にインストール用のドライバー パッケージを作る必要があります。 詳しくは、「[ドライバーのビルド](building-a-driver.md)」と「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。
-   まだ準備ができていない場合は、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」の指示に従ってください。
-   テスト コンピューターの構成とプロビジョニングが済んだら、Visual Studio を使ってドライバーの展開、テストのスケジュール、テスト コンピューター上でのドライバーのデバッグを実行できます。 展開と、ビルド時に自動的にドライバーを展開する方法について詳しくは、「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。

<a name="instructions"></a>手順
------------

### <a name="span-idtotestthedriverinstallationonatestcomputerspanspan-idtotestthedriverinstallationonatestcomputerspanspan-idtotestthedriverinstallationonatestcomputerspanstep-1-to-test-the-driver-installation-on-a-test-computer"></a><span id="To_test_the_driver_installation_on_a_test_computer"></span><span id="to_test_the_driver_installation_on_a_test_computer"></span><span id="TO_TEST_THE_DRIVER_INSTALLATION_ON_A_TEST_COMPUTER"></span>手順 1: テスト コンピューターでドライバーのインストールをテストするには

テスト コンピューターの構成とプロビジョニングが済んだら、ドライバー パッケージ プロジェクトがテスト コンピューターに自動的に展開およびインストールされるように構成することができます。

1.  ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。
2.  ドライバーのプロパティ ページで、**[構成プロパティ]**、**[Driver Install] (ドライバーのインストール)**、**[Deployment] (配置)** の順にクリックします。
3.  **[配置を有効にする]** をオンにします。 詳しくは、「[ドライバー パッケージ プロジェクトの展開プロパティ](deployment-properties-for-driver-projects.md)」をご覧ください。
4.  **[リモート コンピューター]** として構成したテスト コンピューターを選択します。
5.  **[Driver Installation Options (ドライバー インストール オプション)]** で、**[Install and Verify (インストールと確認)]** をクリックし、**[Default Driver Installation Task (既定のドライバー インストール タスク)]** をクリックします。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [ドライバーのテスト](testing-a-driver.md)
 

 






