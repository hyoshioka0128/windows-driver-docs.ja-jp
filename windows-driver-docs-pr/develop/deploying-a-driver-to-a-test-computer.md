---
ms.assetid: 328404BD-E888-4AAA-AA24-B57FD01E9E54
title: テスト コンピューターへのドライバーの展開
description: Visual Studio では、WDK が提供するテスト機能を使って、テスト用コンピューターでドライバーをビルド、展開、デバッグすることができます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 613870a14b456ec66946a628f0ef1785a0202009
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370768"
---
# <a name="deploying-a-driver-to-a-test-computer"></a>テスト コンピューターへのドライバーの展開

Visual Studio 開発環境の利点を利用して、WDK は、テスト コンピューター上でドライバーのビルド、展開、デバッグができるようにするテスト機能を提供します。 WDK を使ってテスト システムにドライバーを適切に展開するには、まず、テスト コンピューターをセットアップし、構成する必要があります。 ドライバーをさまざまなテスト シナリオでテストする場合は、複数のコンピューターをセットアップして構成できます。

## <a name="span-idsetting_up_the_test_computerspanspan-idsetting_up_the_test_computerspanspan-idsetting_up_the_test_computerspansetting-up-the-test-computer"></a><span id="Setting_up_the_test_computer"></span><span id="setting_up_the_test_computer"></span><span id="SETTING_UP_THE_TEST_COMPUTER"></span>テスト コンピューターのセットアップ


-   「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」の手順に従ってください。

**注**  テスト コンピューターの設定に関して問題が発生した場合は、「[ドライバーの展開、テスト、およびデバッグに関する構成のトラブルシューティング](troubleshooting-configuration-of-driver-deployment--testing-and-debugging.md)」をご覧ください。

 

## <a name="span-idsetting_deployment_properties_for_your_driver_solutionspanspan-idsetting_deployment_properties_for_your_driver_solutionspanspan-idsetting_deployment_properties_for_your_driver_solutionspansetting-deployment-properties-for-your-driver-solution"></a><span id="Setting_deployment_properties_for_your_driver_solution"></span><span id="setting_deployment_properties_for_your_driver_solution"></span><span id="SETTING_DEPLOYMENT_PROPERTIES_FOR_YOUR_DRIVER_SOLUTION"></span>ドライバー ソリューションの展開プロパティの設定


ドライバー プロジェクトのプロパティ ページで、ドライバーのテスト用の展開方法を細かく制御できます。 各構成でドライバー ソリューションをビルドするたびに、自動的にドライバーが展開されるようにすることができます。

1.  ドライバー プロジェクトのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、 **[構成プロパティ]** 、 **[Driver Install (ドライバーのインストール)]** 、 **[配置]** の順にクリックします。
3.  構成済みのテスト コンピューターを選択するか、テスト用に構成するコンピューターの名前を選択します。 「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

    ドライバー パッケージ プロジェクトの展開を有効にすると、ソリューションのビルド時に選ばれたテスト コンピューターにドライバーが自動的に展開されます。 ドライバーのインストールと展開に必要なオプションは、 **[展開]** プロパティ ページを使って構成できます。 「[ドライバー パッケージ プロジェクトの展開プロパティ](deployment-properties-for-driver-projects.md)」をご覧ください。

4.  テスト コンピューターへの展開を有効にする際は、テストの効果を高めるために、テスト コンピューター上で[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)、KMDF 検証ツール、UMDF 検証ツールを自動的に有効化し、構成することもできます。 ドライバー パッケージ プロジェクトに対してこれらのオプションを設定するには、 **[構成プロパティ]** 、 **[ドライバーのインストール]** の順にクリックし、次のプロパティ ページをクリックします。
    -   [ドライバー パッケージ プロジェクトのドライバーの検証ツール プロパティ](driver-verifier-properties-for--driver-projects.md)
    -   [ドライバー パッケージ プロジェクトの KMDF 検証ツール プロパティ](kmdf-verifier-properties-for-driver-package-projects.md)
    -   [ドライバー パッケージ プロジェクトの UMDF 検証ツール プロパティ](umdf-verifier-properties-for-driver-package-projects.md)

## <a name="span-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanspan-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanspan-idbuilding_a_driver_and_deploying_the_driver_to__test_computerspanbuilding-a-driver-and-deploying-the-driver-to-test-computer"></a><span id="Building_a_driver_and_deploying_the_driver_to__test_computer"></span><span id="building_a_driver_and_deploying_the_driver_to__test_computer"></span><span id="BUILDING_A_DRIVER_AND_DEPLOYING_THE_DRIVER_TO__TEST_COMPUTER"></span>ドライバーのビルドと、テスト コンピューターへのドライバーの展開


1.  ドライバーを展開する前に、ドライバー ソリューションをビルドできることを確認します。 ドライバー ソリューションには、ドライバーをテスト コンピューターにインストールできるようにするために、ドライバーとドライバー パッケージが含まれている必要があります。 詳しくは、「[ドライバー パッケージの作成](creating-a-driver-package.md)」と「[ドライバーのビルド](building-a-driver.md)」をご覧ください。
2.  また、テスト コンピューターにドライバーを展開する際は、あらかじめドライバー パッケージに署名しておく必要があります。 「[開発中とテスト中のドライバーへの署名](signing-a-driver-during-development-and-testing.md)」をご覧ください。
3.  構成したテスト コンピューターを選びます。
4.  ドライバーを展開するには、 **[ビルド]** メニューの **[ソリューションのビルド]** または **[ソリューションの配置]** をクリックします。ビルドと展開を行って、デバッグを開始するには、**F5** キーを押します。
5.  テスト コンピューターでは、変更が必要であることの確認を求めるダイアログ ボックスが表示される場合があります。  その場合、確認するまで展開は一時停止します。

ドライバーを展開すると、テスト コンピューターの %Systemdrive%\\drivertest\\drivers フォルダーにドライバー ファイルがコピーされます。 展開中に何か異変に気付いた場合は、テスト コンピューターにファイルがコピーされているかどうかを確認してください。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\\drivertest\\drivers フォルダーに存在することを確認します。

## <a name="span-idtroubleshooting_driver_deployment_spanspan-idtroubleshooting_driver_deployment_spanspan-idtroubleshooting_driver_deployment_spantroubleshooting-driver-deployment"></a><span id="Troubleshooting_driver_deployment_"></span><span id="troubleshooting_driver_deployment_"></span><span id="TROUBLESHOOTING_DRIVER_DEPLOYMENT_"></span>ドライバー展開のトラブルシューティング


ここでは、Visual Studio と WDK を使っている場合に、テスト コンピューターへのドライバー展開をトラブルシューティングする際のヒントをいくつか示します。

**展開がエラー コード2 で失敗する**

次のレジストリ キーを追加します。

**HKLM\Software\Microsoft\DriverTest\Service**

このキーの下に DWORD 値 **DebugSession** を作成し、0 に設定します。

この値を設定する必要があるのは 1 回だけであり、値は将来の展開まで保持されます。


<span id="Can_t_find_the_deployment_properties_for_the_driver_project"></span><span id="can_t_find_the_deployment_properties_for_the_driver_project"></span><span id="CAN_T_FIND_THE_DEPLOYMENT_PROPERTIES_FOR_THE_DRIVER_PROJECT"></span>**ドライバー プロジェクトの展開プロパティが見つからない**  
展開プロパティは、ドライバー パッケージがある場合のみ使うことができます。 ドライバー ソリューションにドライバー パッケージ プロジェクトがない場合は、追加する必要があります。 ドライバー パッケージには、インストールに必要な INF ファイルなどのコンポーネントが含まれています。 詳しくは、「[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)」と「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。

ドライバー パッケージを追加したら、ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックして **[プロパティ]** をクリックします。 ドライバー パッケージのプロパティ ページで、 **[構成プロパティ]** 、 **[ドライバーのインストール]** 、 **[展開]** の順にクリックします。

<span id="Problems_selecting__configuring_or_locating_the_target_computer"></span><span id="problems_selecting__configuring_or_locating_the_target_computer"></span><span id="PROBLEMS_SELECTING__CONFIGURING_OR_LOCATING_THE_TARGET_COMPUTER"></span>**ターゲット コンピューターを選択、構成、または特定する際の問題**  
Windows Driver Kit (WDK) 8.1 と Windows Driver Kit (WDK) 8 を使ってターゲット コンピューターをセットアップする手順については、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。 ターゲット コンピューターのプロビジョニングで問題が発生した場合は、「[ドライバーの展開、テスト、およびデバッグに関する構成のトラブルシューティング](troubleshooting-configuration-of-driver-deployment--testing-and-debugging.md)」をご覧ください。

ターゲット コンピューターで N バージョンまたは KN バージョンの Windows を実行している場合は、N バージョンと KN バージョンの Windows 用の Media Feature Pack をインストールする必要があります。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」をご覧ください。

<span id="Problems_installing_the_driver_on_64-bit_version_of_Windows"></span><span id="problems_installing_the_driver_on_64-bit_version_of_windows"></span><span id="PROBLEMS_INSTALLING_THE_DRIVER_ON_64-BIT_VERSION_OF_WINDOWS"></span>**64 ビット バージョンの Windows にドライバーをインストールする際の問題**  
Windows Vista 以降、すべての 64 ビット バージョンの Windows では、読み込むドライバーのデジタル署名がドライバー コードに必要です。 「[ドライバーへの署名](signing-a-driver.md)」と「[開発中とテスト中のドライバーへの署名](signing-a-driver-during-development-and-testing.md)」をご覧ください。

<span id="Problems_installing_the_driver__general_"></span><span id="problems_installing_the_driver__general_"></span><span id="PROBLEMS_INSTALLING_THE_DRIVER__GENERAL_"></span>**ドライバーをインストールする際の問題 (一般)**  
WDK では、ドライバー パッケージをテスト コンピューターに展開およびインストールできますが、インストールに必要なすべてのコンポーネント (INF ファイルなど) がドライバーにある場合だけです。 詳しくは、「[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)」をご覧ください。 Visual Studio と WDK の外部にドライバーをインストールできることを確認してください。 たとえば、デバイス コンソール ユーティリティの [Devcon](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon) を使って、ドライバーをインストールできるかどうかをテストします。 デバイス (存在する場合) がターゲット コンピューターに接続されていることを確認します。 詳しくは、「[デバイスとドライバーのインストール](https://docs.microsoft.com/windows-hardware/drivers/install/index)」と「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。
