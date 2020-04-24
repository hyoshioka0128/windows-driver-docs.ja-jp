---
ms.assetid: f5676c9c-b582-47d0-9b7c-02b6443103ad
title: WDK を使ったドライバーのビルド
description: このトピックでは、Windows Driver Kit (WDK) でドライバーをビルドする方法について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db6f4fa3a257c04f317ad5569b3d9c444dc1dc0
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "74261422"
---
# <a name="building-a-driver-with-visual-studio-and-the-wdk"></a>Visual Studio と WDK でのドライバーのビルド

このトピックでは、Windows Driver Kit (WDK) でドライバーをビルドする方法について説明します。 WDK 10 は、Microsoft Visual Studio と完全に統合されています。 ドライバーのビルドは、Visual Studio 開発環境を使って行うか、Microsoft Build Engine ([MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)) を使ってコマンド ラインから直接行うことができます。

Microsoft Visual Studio 2015 では、Microsoft Visual Studio Community 2015 を含む任意のエディションを使って、次のシステム用のドライバーをビルドできます。

-   Windows 10
-   Windows 8.1
-   Windows 7

**重要**  Windows Driver Kit (WDK) 8 以降では、Windows ビルド ユーティリティ (Build.exe) は MSBuild に置き換えられました。 現在の WDK は、Visual Studio プロジェクトをビルドする場合と同じコンパイラとビルド ツールを使います。 以前のバージョンの WDK でビルドしたドライバー プロジェクトは、Visual Studio 環境で動作するように変換する必要があります。 変換ユーティリティは、コマンド ラインから実行できます。既にあるソースから新しい Visual Studio プロジェクトを作成することによって、既にあるドライバーを変換することもできます。 詳しくは、「[既にあるソース ファイルからのドライバーの作成](creating-a-driver-from-existing-source-files.md)」と「[WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)」をご覧ください。

 

## <a name="span-idbuilding_a_driver_using_visual_studiospanspan-idbuilding_a_driver_using_visual_studiospanbuilding-a-driver-using-visual-studio"></a><span id="building_a_driver_using_visual_studio"></span><span id="BUILDING_A_DRIVER_USING_VISUAL_STUDIO"></span>Visual Studio を使ったドライバーのビルド


ドライバーのビルドは、Visual Studio でプロジェクトまたはソリューションをビルドする方法と同じです。 Windows ドライバー テンプレートを使って新しいドライバー プロジェクトを作成する場合は、テンプレートによって既定の (アクティブな) プロジェクト構成と既定の (アクティブな) ソリューション ビルド構成が定義されます。

**注**  WDK 8 や Windows Driver Kit (WDK) 8.1 を使って作成したプロジェクトやソリューションを、Windows Driver Kit (WDK) 10 と Visual Studio 2015 で動作するように変換できます。 プロジェクトやソリューションを開く前に、[ProjectUpgradeTool](https://docs.microsoft.com/windows-hardware/drivers/devtest/projectupgradetool) を実行してください。 ProjectUpgradeTool はプロジェクトとソリューションを変換し、WDK 10 を使って構築できるようにします。

 

ビルド構成の管理と編集について詳しくは、「[Visual Studio でのビルド](https://go.microsoft.com/fwlink/p/?linkid=227872)」をご覧ください。

既定のソリューション ビルド構成は、 **[デバッグ]** と **[Win32]** です。 

**構成を選択してドライバーをビルドするには**

1.  同じバージョンの SDK と WDK がコンピューターにインストールされていることを確認します。
2.  Visual Studio で、ドライバー プロジェクトまたはソリューションを開きます。
3.  **[ソリューション エクスプローラー]** でソリューションを右クリックし、 **[構成マネージャー]** をクリックします。
4.  **[構成マネージャー]** で、ビルドの種類に応じて、**アクティブ ソリューション構成** (たとえば **[デバッグ]** 、 **[リリース]** など) と**アクティブ ソリューション プラットフォーム** (たとえば **[Win32]** など) を選びます。
5.  Avshws プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  **[Driver Settings (ドライバーの設定)] > [全般]** に移動し、 **[ターゲットの OS バージョン]** と **[ターゲット プラットフォーム]** を設定します。
6.  ドライバーまたはドライバー パッケージのためのプロジェクト プロパティを構成します。 展開、ドライバー署名、その他のタスクのプロパティを設定できます。 詳しくは、「[ドライバーとドライバー パッケージのためのプロジェクト プロパティの構成](#configure_project_props)」をご覧ください。
7.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします (**Ctrl + Shift + B**)。

## <a name="span-idbuilding_a_driver_using_the_command_line__msbuild_spanspan-idbuilding_a_driver_using_the_command_line__msbuild_spanbuilding-a-driver-using-the-command-line-msbuild"></a><span id="building_a_driver_using_the_command_line__msbuild_"></span><span id="BUILDING_A_DRIVER_USING_THE_COMMAND_LINE__MSBUILD_"></span>コマンド ライン (MSBuild) を使ったドライバーのビルド


**Visual Studio のコマンド プロンプト** ウィンドウと Microsoft Build Engine ([MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)) を使って、コマンドラインからドライバーをビルドできます。

**Visual Studio のコマンド プロンプト ウィンドウを使ってドライバーをビルドするには**

1.  **[開発者コマンド プロンプト for VS2015]** ウィンドウを開きます。

    このウィンドウで MSBuild.exe を使い、プロジェクト (.VcxProj) またはソリューション (.Sln) ファイルを指定して、任意の Visual Studio プロジェクトをビルドできます。

2.  プロジェクト ディレクトリに移動し、ターゲットに対する **MSbuild** コマンドを入力します。

    たとえば、既定のプラットフォームと構成を使って、MyDriver.vcxproj という名前の Visual Studio ドライバー プロジェクトのクリーンなビルドを行うには、プロジェクト ディレクトリに移動し、次の MSBuild コマンドを入力します:

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj
    ```

    **構文** - 特定の構成とプラットフォームを指定するには、次のコマンド構文を使います。

    ```cpp
    msbuild /t:clean /t:build ProjectFile /p:Configuration=<Debug|Release> /p:Platform=architecture /p:TargetPlatformVersion=a.b.c.d /p:TargetVersion=OS    
    ```

    たとえば、次のコマンドでは、構成が "Debug" でプラットフォームが "Win32" の、Windows 10 を対象としたユニバーサル Windows ドライバーをビルドします。

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj /p:Configuration="Debug" /p:Platform=Win32 /p:TargetVersion=”Windows10” /p:TargetPlatformVersion=”10.0.10010.0”
    ```

    **TargetPlatformVersion** 設定は省略可能ですが、これにより、ビルドに使うキットのバージョンを指定できます。 既定では、最新のキットを使用します。

## <a name="span-idconfigure_project_propsspanspan-idconfigure_project_propsspanconfiguring-project-properties-for-your-driver-and-driver-package"></a><span id="configure_project_props"></span><span id="CONFIGURE_PROJECT_PROPS"></span>ドライバーとドライバー パッケージのためのプロジェクト プロパティの構成


**プロパティ ページ**を使って、ドライバーとドライバー パッケージのオプションの構成と設定を行います。 ドライバーの構成では、ソリューションのビルド時に自動的に署名するかどうかと、リモート テスト コンピューターに自動的に展開するかどうかを選ぶことができます。

WDK には、[Stampinf](https://docs.microsoft.com/windows-hardware/drivers/devtest/stampinf)、[WPP プリプロセッサ (WPP トレース)](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-preprocessor) など、多くのコマンド ライン ツールが用意されています。これらは通常、ビルド プロセスに含まれます。 これらのツールは、Visual Studio には同梱されていません。 これらのツールは、Visual Studio ビルド環境に組み込むために、[MSBuild の WDK タスク](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-tasks-for-msbuild)としてラップされています。 いずれかのドライバー テンプレートを使うか、変換した既存のドライバーがある場合は、これらのプロパティ ページが既にプロジェクトに存在していることがあります。 そうでない場合は、関連するファイルの種類 (たとえば、メッセージ コンパイラの .mc や .man ファイル) をプロジェクトやソリューションに追加すると、プロパティ ページがプロジェクトに自動的に追加されます。 詳しくは、「[WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)」をご覧ください。

個別のドライバーまたはドライバー パッケージ全体のプロパティを設定できます。 次の表は、特にドライバーとドライバー パッケージに対して構成できる、利用可能なプロパティの一部を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ドライバー プロジェクトのプロパティ</th>
<th align="left">ドライバ パッケージのプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>個別のドライバー ファイルの署名プロパティ (「<a href="signing-a-driver.md" data-raw-source="[Signing a Driver](signing-a-driver.md)">ドライバーの署名</a>」をご覧ください)</p></td>
<td align="left"><p>ドライバー パッケージの署名プロパティ (「<a href="signing-a-driver.md" data-raw-source="[Signing a Driver](signing-a-driver.md)">ドライバーの署名</a>」をご覧ください)</p></td>
</tr>
<tr class="even">
<td align="left"><a href="counters-manifest-preprocessor-properties-for-driver-projects.md" data-raw-source="[Counters Manifest Preprocessor Properties for Driver Projects](counters-manifest-preprocessor-properties-for-driver-projects.md)">ドライバー プロジェクトのカウンター マニフェスト プリプロセッサ プロパティ</a> (<a href="https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp" data-raw-source="[CTRPP](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp)">CTRPP</a> 用)</td>
<td align="left"><p><a href="deployment-properties-for-driver-projects.md" data-raw-source="[Deployment Properties for Driver Package Projects](deployment-properties-for-driver-projects.md)">ドライバー パッケージ プロジェクトの展開プロパティ</a> (「<a href="deploying-a-driver-to-a-test-computer.md" data-raw-source="[Deploying a Driver to a Test Computer](deploying-a-driver-to-a-test-computer.md)">テスト コンピューターへのドライバーの展開</a>」をご覧ください)</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="driver-model-settings-properties-for-driver-projects.md" data-raw-source="[Driver Model Settings Properties for Driver Projects](driver-model-settings-properties-for-driver-projects.md)">ドライバー プロジェクトのドライバー モデル設定プロパティ</a></td>
<td align="left"><p><a href="driver-verifier-properties-for--driver-projects.md" data-raw-source="[Driver Verifier Properties for Driver Package Projects](driver-verifier-properties-for--driver-projects.md)">ドライバー パッケージ プロジェクトのドライバーの検証ツール プロパティ</a></p></td>
</tr>
<tr class="even">
<td align="left"><a href="message-compiler-properties-for-driver-projects.md" data-raw-source="[Message Compiler Properties for Driver Projects](message-compiler-properties-for-driver-projects.md)">ドライバー プロジェクトのメッセージ コンパイラ プロパティ</a></td>
<td align="left"><p><a href="kmdf-verifier-properties-for-driver-package-projects.md" data-raw-source="[KMDF Verifier Properties for Driver Package Projects](kmdf-verifier-properties-for-driver-package-projects.md)">ドライバー パッケージ プロジェクトの KMDF 検証ツール プロパティ</a></p></td>
</tr>
<tr class="odd">
<td align="left"><a href="stampinf-properties-for-driver-projects.md" data-raw-source="[Stampinf Properties for Driver Projects](stampinf-properties-for-driver-projects.md)">ドライバー プロジェクトの Stampinf プロパティ</a></td>
<td align="left"><p><a href="umdf-verifier-properties-for-driver-package-projects.md" data-raw-source="[UMDF Verifier Properties for Driver Package Projects](umdf-verifier-properties-for-driver-package-projects.md)">ドライバー パッケージ プロジェクトの UMDF 検証ツール プロパティ</a></p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-preprocessor" data-raw-source="[WPP Preprocessor (WPP Tracing)](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-preprocessor)">WPP プリプロセッサ (WPP トレース)</a></td>
<td align="left"><p><a href="inf2cat-properties-for-driver-package-projects.md" data-raw-source="[Inf2Cat Properties for Driver Package Projects](inf2cat-properties-for-driver-package-projects.md)">ドライバー パッケージ プロジェクトの Inf2Cat プロパティ</a> (<a href="../devtest/inf2cat.md" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](../devtest/inf2cat.md)"><strong>Inf2Cat</strong></a> ツールに関するトピックをご覧ください)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtroubleshootingspanspan-idtroubleshootingspantroubleshooting-tip-for-building-a-driver"></a><span id="troubleshooting"></span><span id="TROUBLESHOOTING"></span>ドライバーのビルドに関するトラブルシューティングのヒント


WDK と Visual Studio を使ってドライバーをビルドする際のトラブルシューティングには、以下の情報をお役立てください。

**Visual Studio のオプションを使ってより詳しいビルド出力を得るには**

1.  **[ツール]** &gt; **[オプション]** をクリックします。
2.  **[プロジェクトおよびソリューション]** フォルダーをクリックし、 **[ビルド/実行]** をクリックします。
3.  **[MSBuild プロジェクト ビルドの出力の詳細]** と **[MSBuild プロジェクト ビルド ログ ファイルの詳細]** のオプションを変更します。 既定では、いずれも "最小" に設定されています。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Visual Studio でのビルド](https://go.microsoft.com/fwlink/p/?linkid=227872)
* [異なるバージョンの Windows に対するドライバーのビルド](building-drivers-for-different-versions-of-windows.md)
* [ユーザー モード ドライバーとデスクトップ アプリでの Microsoft C ランタイムの使用](using-the-microsoft-c-runtime-with-user-mode-drivers-and-apps.md)
* [ProjectUpgradeTool](https://docs.microsoft.com/windows-hardware/drivers/devtest/projectupgradetool)
* [MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)
* [既にあるソース ファイルからのドライバーの作成](creating-a-driver-from-existing-source-files.md)
* [WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)
* [ドライバーへの署名](signing-a-driver.md)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)







