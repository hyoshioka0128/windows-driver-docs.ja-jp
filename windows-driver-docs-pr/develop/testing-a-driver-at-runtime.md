---
ms.assetid: 50BF5B17-B7F0-49F2-9ED6-652DB32D638E
title: Visual Studio を使って実行時にドライバーをテストする方法
description: Visual Studio の WDK 拡張機能を使うと、ネットワーク上のテスト コンピューターで簡単にドライバーのビルド、展開、インストール、テストを実行できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f024d689ef60087d854418cb247c8ff28e0265
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261417"
---
# <a name="how-to-test-a-driver-at-runtime-using-visual-studio"></a>Visual Studio を使って実行時にドライバーをテストする方法

WDK 拡張機能は Visual Studio にドライバー テスト インターフェイスを提供して、ネットワーク上のテスト コンピューターで簡単にドライバーのビルド、展開、インストール、テストを実行できるようにします。 WDK にはデバイス ドライバー テストのコレクションが用意されていて、ドライバーの機能のテストに使うことができます。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   インストールの準備ができているドライバー パッケージ。 まずドライバーを作ってビルドし、次にインストール用のドライバー パッケージを作る必要があります。 詳しくは、「[ドライバーのビルド](building-a-driver.md)」と「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。
-   ドライバーはテスト署名されている必要があります。 詳しくは、「[ドライバーへの署名](signing-a-driver.md)」をご覧ください。
-   テスト コンピューター。 テスト コンピューターは、開発に使ったコンピューターと同じネットワーク上にある必要があります。 両方のコンピューターが同じドメインまたは同じワークグループのネットワークに接続されている必要があります。 テスト コンピューターでは、テスト対象のバージョンの Windows が実行されている必要があります。 
-   テスト対象のデバイス。
-   (*推奨*) テスト コンピューターへのカーネル モード デバッグ接続を設定します。 カーネル モード デバッグ用のネットワーク接続を使うには、ターゲット コンピューターで Windows 8 が実行されている必要があります。 Windows 7 または Windows Vista が実行されているコンピューターでは、カーネル モード デバッグ用に USB、1394、シリアル接続を設定できます。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

<a name="instructions"></a>手順
------------

### <a name="span-idconfigure_computers_for_testingspanspan-idconfigure_computers_for_testingspanspan-idconfigure_computers_for_testingspanstep-1-configure-computers-for-testing"></a><span id="Configure_computers_for_testing"></span><span id="configure_computers_for_testing"></span><span id="CONFIGURE_COMPUTERS_FOR_TESTING"></span>ステップ 1:テスト用にコンピューターを構成する

Visual Studio から、テスト用のコンピューターの構成とプロビジョニングを行うことができます。 テスト コンピューターを構成すると、WDK ドライバー テスト フレームワークは自動的にテスト コンピューターのリモート デバッグを有効にして、必要なテスト バイナリとサポート ファイルを転送します。

1.  まだ準備ができていない場合は、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の指示に従ってください。
2.  テストするデバイスを、テスト コンピューターに接続します。

テスト コンピューターの構成とプロビジョニングが済んだら、Visual Studio を使ってドライバーの展開、テストのスケジュール、テスト コンピューター上でのドライバーのデバッグを実行できます。 展開と、ビルド時に自動的にドライバーを展開する方法について詳しくは、「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。

[ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) (実行時にドライバーを検証するツール) を有効にしてオプションを設定することもできます。 ドライバー検証ツールは、テスト コンピューターでテストを実行するときに、ドライバーを監視します。 ドライバーの検証ツールの展開用のオプションの設定について詳しくは、「[ドライバー プロジェクトのドライバーの検証ツール プロパティ](driver-verifier-properties-for--driver-projects.md)」をご覧ください。

Visual Studio 以外でテストを実行することもできます。詳しくは、「[コマンド プロンプトから実行時にドライバーをテストする方法](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)」をご覧ください。 WDK 8.1 以降、コマンド スクリプトを使って、テスト コンピューターで HCK テスト スイートをコピーおよび実行できるようになりました。 「[WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)」をご覧ください。

### <a name="span-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanspan-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanspan-idselect_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__81_spanstep-2-select-an-hck-test-suite-to-run-on-the-test-computer-using-wdk-81"></a><span id="Select_an_HCK_Test_Suite_to_run_on_the_test_computer__using_WDK__8.1_"></span><span id="select_an_hck_test_suite_to_run_on_the_test_computer__using_wdk__8.1_"></span><span id="SELECT_AN_HCK_TEST_SUITE_TO_RUN_ON_THE_TEST_COMPUTER__USING_WDK__8.1_"></span>ステップ 2:テスト コンピューターで実行する HCK テスト スイートを選択する (WDK 8.1 を使う場合)

WDK 8.1 以降では、テスト コンピューターで実行する HCK テスト スイートを選択できるようになりました。 HCK テスト スイートには、[Device Fundamentals テスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/device-fundamentals-tests)や、グラフィックス、イメージング、ワイヤレス LAN、モバイル ブロードバンド (CDMA と GSM)、WiFi Direct デバイス用の Windows ハードウェア認定キット (HCK) テストが含まれています。

-   「[WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)」をご覧ください。

### <a name="span-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanspan-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanspan-idselect_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_81_spanstep-3-select-the-tests-to-run-on-the-test-computer-wdk-8-and-wdk-81"></a><span id="Select_the_tests_to_run_on_the_test_computer__WDK_8_and_WDK_8.1_"></span><span id="select_the_tests_to_run_on_the_test_computer__wdk_8_and_wdk_8.1_"></span><span id="SELECT_THE_TESTS_TO_RUN_ON_THE_TEST_COMPUTER__WDK_8_AND_WDK_8.1_"></span>ステップ 3:テスト コンピューターで実行するテストを選択する (WDK 8 と WDK 8.1)

さまざまなテスト対象でのドライバーのテストを簡単にするため、テストは*テスト グループ*と呼ばれる単位でテスト システムに対して実行するようにスケジュールされます。 ドライバー テスト グループは、テスト コンピューターで実行するよう選択したテストのコレクションです。 ドライバー テスト グループを使うと、テストや各テスト成功の結果を整理しやすくなります。 テスト結果は個別のフォルダーに保存できます。 テスト グループの作成と管理、テスト グループ内でテストに渡すパラメーターの変更、テスト システムに対するテスト実行のスケジュールを行うことができます。

1.  **[ドライバー]** メニューで、 **[テスト]** 、 **[Test Group Explorer] (テスト グループ エクスプローラー)** の順にクリックします。
2.  **[Driver Test Group Explorer (ドライバー テスト グループ エクスプローラー)]** ウィンドウで、 **[Create a new test group (新しいテスト グループの作成)]** ボタンをクリックします。 または、 **[Driver (ドライバー)]** メニューの **[New Test Group (新しいテスト グループ)]** をクリックします。
3.  作成したグループの **[Driver Test Group (ドライバー テスト グループ)]** ウィンドウで、 **[Test Group Name (テスト グループ名)]** ボックスにグループを識別する名前を入力します。 既定の名前は Driver Test Group\_*nnnnn* です。*nnnnn* は、このテスト グループの番号を表します
4.  **[Add/Remove Tests (テストの追加と削除)]** をクリックします。
5.  **[Add or Remove Driver Tests] (ドライバー テストの追加または削除)** ダイアログ ボックスで、ドライバー テストのカテゴリとアーキテクチャ (すべて、x86、x64、ARM) を指定できます。 既定ではすべてのテストが表示されます。 テストのカテゴリを表示するには、[Driver Test Categories] (ドライバー テスト カテゴリ) ドロップダウン リスト内のフォルダーをクリックします。

    たとえば、WDK 8 において [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) で使われるすべての Device Fundamental テストを選ぶには、 **[すべてのテスト]** 、 **[Certification]** (認定)、 **[Device Fundamentals]** (Device Fundamental) の順にクリックします。 テストについて詳しくは、「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。

    WDK 8.1 では、Device Fundamentals テストは **[All Tests (すべてのテスト)]** 、 **[HCK Tests (HCK テスト)]** 、 **[Certification (認定)]** の下の **[Device Fundamentals (Device Fundamentals)]** フォルダーにあります。 WDK 8.1 では、[Driver Test Categories] (ドライバー テスト カテゴリ) に HCK (基本) テストが含まれています。 詳しくは、「[WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)」をご覧ください。

6.  目的とするテスト コンピューターのアーキテクチャ (x86、x64、ARM) に対応したテストを必ず選択してください。 **[Architecture Filter (アーキテクチャ フィルター)]** を使って、テスト コンピューターで動作するテストだけを表示します。
7.  [ **&gt;&gt;** ] をクリックして、選択したテストを追加します。

### <a name="span-idconfigure_test_parametersspanspan-idconfigure_test_parametersspanspan-idconfigure_test_parametersspanstep-4-configure-test-parameters"></a><span id="Configure_test_parameters"></span><span id="configure_test_parameters"></span><span id="CONFIGURE_TEST_PARAMETERS"></span>ステップ 4:テスト パラメーターを構成する

テスト グループのテストを選んだら、ドライバー テストに渡される任意のランタイム パラメーターを構成できます。 たとえば、多くの Device Fundamental テストには、デバイスの照会を表すパラメーター *DQ* があります。 これは、[Simple Data Evaluation Language](https://docs.microsoft.com/windows-hardware/drivers/wdtf/simple-data-evaluation-language-overview) (SDEL) クエリです。 [Windows ドライバー テスト フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdtf/index)には、属性や関係に基づいたターゲット収集タスクを簡略化するためのクエリ言語として、SDEL が用意されています。

たとえば、USB デバイスのみにテストを実行するには、デバイス クエリ class='usb' を使います。 テスト グループ内の各テスト パラメーターの値は変更できます。

1.  **[Driver Test Group (ドライバー テスト グループ)]** ウィンドウでテスト名をクリックすることで、テストのすべての実行時テスト パラメーターを表示および編集できます。 **[Driver Test Group (ドライバー テスト グループ)]** ウィンドウには、選択したテストとテスト パラメーターの説明が表示されます。 テスト パラメーターの設定について詳しくは、「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。
2.  テストを選択してパラメーターを設定し、グループに名前を付けたら、 **[保存]** をクリックします。

    テスト グループを保存すると、このテスト グループが現在選択されているテスト グループになり、テスト グループ名が [Driver Test] (ドライバー テスト) ツール バーに表示されます。 これで、現在選択されているリモート テスト コンピューター ([Driver Test (ドライバー テスト)] ツール バーに表示されています) に対してテストを実行できます。

### <a name="span-idbuild_and_deploy_the_driverspanspan-idbuild_and_deploy_the_driverspanspan-idbuild_and_deploy_the_driverspanstep-5-build-and-deploy-the-driver"></a><span id="Build_and_deploy_the_driver"></span><span id="build_and_deploy_the_driver"></span><span id="BUILD_AND_DEPLOY_THE_DRIVER"></span>ステップ 5:ドライバーをビルドして展開する

-   **[ビルド]** メニューの **[ソリューションの配置]** をクリックします。

ビルド時に自動的にドライバーを展開する方法について詳しくは、「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。 テスト コンピューターでのドライバーの検証ツール オプションの自動設定について詳しくは、「[ドライバー プロジェクトのドライバーの検証ツール プロパティ](driver-verifier-properties-for--driver-projects.md)」をご覧ください。 テスト コンピューターで、ドライバーの検証ツールを常に有効にしておく必要があります。

### <a name="span-idrun_the_tests_on_the_test_computerspanspan-idrun_the_tests_on_the_test_computerspanspan-idrun_the_tests_on_the_test_computerspanstep-6-run-the-tests-on-the-test-computer"></a><span id="Run_the_tests_on_the_test_computer"></span><span id="run_the_tests_on_the_test_computer"></span><span id="RUN_THE_TESTS_ON_THE_TEST_COMPUTER"></span>ステップ 6:テスト コンピューターでテストを実行する

-   **[ドライバー]** メニューで、 **[テスト] &gt; [テストの実行]** の順にクリックします。 [テストの実行] は既定で、現在選択されているテスト グループのすべてのテストを実行します。

<a name="remarks"></a>注釈
-------

ドライバー テストとテスト カテゴリについて詳しくは、「[Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)」をご覧ください。 テスト フレームワークについて詳しくは、「[Test Authoring and Execution Framework](https://docs.microsoft.com/windows-hardware/drivers/taef/index) (TAEF)」と「[Windows ドライバー テスト フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdtf/index) (WDTF)」をご覧ください。

独自のドライバー テストを作成して、テスト コンピューターに展開することができます。 詳しくは、「[ドライバー テストを作成する方法](how-to-write-a-driver-test-.md)」をご覧ください。

開発サイクルの初期に Visual Studio で Device Fundamental テストを実行しておくと、最終的に [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) を使ってドライバーをテストする際の負担を減らすことができます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [WDK 8.1 の HCK テスト スイートを実行する方法](run-the-hck-test-suites-in-the-wdk.md)
* [Device Fundamental テストを選んで構成する方法](how-to-select-and-configure-the-device-fundamental-tests.md)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [Windows のデバッグの概要](https://docs.microsoft.com/windows-hardware/drivers/debugger/getting-started-with-windows-debugging)
* [ハードウェア認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227016)
* [Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)
* [コマンド プロンプトから実行時にドライバーをテストする方法](how-to-test-a-driver-at-runtime-from-a-command-prompt.md)
 

 






