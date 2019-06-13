---
ms.assetid: 7193DA4B-2461-4E00-90B4-C31B93C8E9BD
title: ドライバー パッケージ プロジェクトの展開プロパティ
description: プロジェクトの各構成で、リモート テスト コンピューターにドライバー パッケージを自動的に展開するように構成できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4790fa57c877d9b74a2bd46fc80cef87528a20a5
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63356632"
---
# <a name="deployment-properties-for-driver-package-projects"></a>ドライバー パッケージ プロジェクトの展開プロパティ

プロジェクトの各構成で、リモート テスト コンピューターにドライバー パッケージを自動的に展開するように構成できます。 ドライバーのプロジェクト プロパティ ページで、ドライバーのテスト用の展開方法を細かく制御できます。 各構成でドライバー ソリューションをビルドするたびに、自動的にドライバーが展開されるようにすることができます。 展開について詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」と「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。

## <a name="span-idsettingdeploymentpropertiesfordriverpackageprojectsspanspan-idsettingdeploymentpropertiesfordriverpackageprojectsspanspan-idsettingdeploymentpropertiesfordriverpackageprojectsspansetting-deployment-properties-for-driver-package-projects"></a><span id="Setting_deployment_properties_for_driver_package_projects"></span><span id="setting_deployment_properties_for_driver_package_projects"></span><span id="SETTING_DEPLOYMENT_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>ドライバー パッケージ プロジェクトの展開プロパティの設定


1.  ドライバー パッケージのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。

    **注**  ドライバー ソリューションにドライバー パッケージ プロジェクトがない場合は、追加する必要があります。 「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。 展開プロパティは、ドライバー パッケージがある場合のみ使うことができます。
2.  ドライバー パッケージのプロパティ ページで、 **[構成プロパティ]** 、 **[ドライバーのインストール]** 、 **[展開]** の順にクリックします。
3.  **[配置を有効にする]** をオンにします。 このオプションがオンになっている場合は、使用するテスト コンピューターを選ぶことができ、ドライバーのインストールと展開のオプションを構成できます。

## <a name="span-idprojectconfigurationandplatformspanspan-idprojectconfigurationandplatformspanspan-idprojectconfigurationandplatformspanproject-configuration-and-platform"></a><span id="Project_Configuration_and_Platform"></span><span id="project_configuration_and_platform"></span><span id="PROJECT_CONFIGURATION_AND_PLATFORM"></span>プロジェクト構成とプラットフォーム


構成一覧とプラットフォーム一覧を使うと、さまざまなプロジェクト構成とプラットフォームの組み合わせに、さまざまな展開の設定を適用できます。 たとえば、1 台のテスト コンピューターにはデバッグ用ビルドのための展開オプションのセットを使ってドライバーを展開し、別のテスト コンピューターにはリリース用ビルドのための展開オプションを使うことができます。

## <a name="span-idenablingdeploymentspanspan-idenablingdeploymentspanspan-idenablingdeploymentspanenabling-deployment"></a><span id="Enabling_deployment"></span><span id="enabling_deployment"></span><span id="ENABLING_DEPLOYMENT"></span>展開の有効化


ドライバー パッケージをテスト コンピューターに展開するには、 **[配置を有効にする]** をオンにします。 構成一覧と組み合わせて、デバッグ用ビルドの展開を無効にし、リリース用ビルドの展開を有効にすることもできます。

確実にドライバーの最新バージョンをテストできるようにするには、 **[Remove previous driver versions before deployment]** (展開前にドライバーの以前のバージョンを削除する) を選択します。

## <a name="span-idtargetcomputernamespanspan-idtargetcomputernamespanspan-idtargetcomputernamespantarget-computer-name"></a><span id="Target_computer_name"></span><span id="target_computer_name"></span><span id="TARGET_COMPUTER_NAME"></span>ターゲット コンピューター名


展開とテストに使うターゲット コンピューターを選ぶことができます。 テスト コンピューターを構成済みの場合は、この一覧から選ぶことができます。 テスト コンピューターが構成されていない場合は、 **[参照]** ボタンを使って構成できます。 テスト コンピューターの構成について詳しくは、「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。 プロジェクト構成とプラットフォームが、テスト システムのターゲット アーキテクチャと必ず一致するようにしてください。 よく発生する展開エラーは、x64 バージョンの Windows を実行しているシステムに x86 (Win32) ドライバーをインストールしようとする場合です。 テスト コンピューターを構成するときに、カーネル モード デバッガーを実行することもできます。 詳しくは、「[Setting Up Kernel-Mode Debugging in Visual Studio (Visual Studio でのカーネル モード デバッグの設定)](https://msdn.microsoft.com/windows/hardware/hh439376)」をご覧ください。

## <a name="span-iddriverinstallationoptionsspanspan-iddriverinstallationoptionsspanspan-iddriverinstallationoptionsspandriver-installation-options"></a><span id="Driver_installation_options"></span><span id="driver_installation_options"></span><span id="DRIVER_INSTALLATION_OPTIONS"></span>ドライバーのインストールのオプション


**[インストールしない] -** これが既定のオプションです。 ドライバー パッケージを[ドライバー ストア](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544868)にインポートしている場合や、テスト コンピューター上でドライバーの検証ツールのオプションの有効化と設定を行っている場合は、インストールしないことを選択できます。

**[Hardware ID Driver Update] (ハードウェア ID のドライバーの更新) -** 実際のハードウェア デバイスのドライバーを展開するには、このオプションではなく、 **[Install and Verify]** (インストールと確認) を使います。 ルート列挙デバイスのドライバーを展開するには、 **[Hardware ID Driver Update]** (ハードウェア ID のドライバーの更新) と **[Install and Verify]** (インストールと確認) のどちらを使うこともできます。 [Hardware ID Driver Update]\(ハードウェア ID のドライバーの更新\) を使用する場合は、INF ファイルにあるのと同じハードウェア ID を入力する必要があります。ハードウェア ID の形式は、Root\\Xxx であることが必要です。 このオプションを選択すると、ファイルはリモート コンピューターの %*Systemdrive*%\\drivertest\\drivers フォルダーにコピーされます。 デバイス コンソール ユーティリティ [Devcon](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544707) は、そのハードウェア ID のドライバーと INF ファイルをパッケージからインストールします。 たとえば、 **[Hardware ID Driver Update]\(ハードウェア ID のドライバーの更新\)** を選択し、HWID を **Root\\** <em>プロジェクト名</em> に設定できます。 プロジェクト名に含まれているスペースは、すべて除外します。

**[Custom Command Line (カスタム コマンド ライン)] -** インストール時に独自のカスタム コマンド スクリプトを実行する場合に選びます。 カスタム コマンド スクリプトを実行する場合は、 **[追加ファイル]** セクションに必要なファイルを追加します。 追加ファイルは、リモート コンピューターの *%Systemdrive%* \\drivertest\\drivers フォルダーにコピーされます。

**[Install and Verify (インストールと確認)] -** 自動化されたテスト スクリプトを使って、インストールをテストすることができます。 このオプションを選択して、 **[Default Driver Package Installation Task (possible reboot) (既定のドライバー パッケージ インストール タスク (再起動の可能性あり))]** または **[Default Printer Driver Package Installation Task (possible reboot) (既定のプリンター ドライバー パッケージ インストール タスク (再起動の可能性あり))]** を指定すると、テストはドライバーの INF ファイルを読み取って、ドライバーをインストールします。 次に、ドライバーが起動して動作していることを確認します。 テストが完了すると、インストール タスクの成功/失敗に関する詳細情報が提供されます。

**[Optional Device Query (オプションのデバイスの照会)] -** 既定値は *%PathToInf%* です。 ドライバーの INF ファイルへのパスは、自動的に置き換えられます。 INF ファイルを別の場所に置く必要があるのでない限り、この値を変更する必要はありません。

## <a name="span-idadditionalfilesspanspan-idadditionalfilesspanspan-idadditionalfilesspanadditional-files"></a><span id="Additional_Files"></span><span id="additional_files"></span><span id="ADDITIONAL_FILES"></span>追加ファイル


**[追加ファイル]** ボックスを使って、カスタム インストール スクリプトや、リモート テスト コンピューターにコピーするアプリケーションを指定できます。 ここで指定したファイルは、リモート コンピューターの *%Systemdrive%* \\drivertest\\drivers フォルダーに追加されます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
* [Visual Studio を使って実行時にドライバーをテストする方法](testing-a-driver-at-runtime.md)
* [Visual Studio でのカーネル モード デバッグの設定](https://msdn.microsoft.com/windows/hardware/hh439376)
 

 






