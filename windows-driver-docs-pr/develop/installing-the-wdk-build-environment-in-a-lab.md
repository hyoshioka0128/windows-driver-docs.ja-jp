---
ms.assetid: D4B35683-5BD1-40F8-9734-95DADF9E0F20
title: ラボに WDK ビルド環境をインストールする
description: Windows Driver Kit (WDK) 8.1 では、Visual Studio と WDK のコンポーネントを新しい場所にコピーして、コマンド ラインからビルド環境を実行できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5072737d94c1546f29953147edbdf8b44304929d
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63344855"
---
# <a name="installing-the-wdk-81-build-environment-in-a-lab"></a>ラボに WDK 8.1 ビルド環境をインストールする

Windows Driver Kit (WDK) 8.1 には、Visual Studio と WDK のコンポーネントを新しい場所にコピーして、コマンド ラインからビルド環境を実行できるようにする機能が用意されています。 この場所から、Visual Studio や WDK のインストール プログラムを実行することなく Windows ドライバーをビルドできます。

WDK をビルド プロセスに統合する必要がある場合や、ビルド プロセスをラボ環境またはテスト環境に配布する場合は、この機能が役に立つ可能性があります。

**注**  この機能を使用できるのは、C および C++ を使うドライバーやアプリケーションをビルドする場合だけです。 マネージ コードや UWP アプリで使うことはできません。


## <a name="1-download-the-visual-studio-and-wdk-and-sdk-setup-files"></a>1. Visual Studio、WDK、SDK のセットアップ ファイルのダウンロード


この機能を有効にするセットアップ スクリプトを実行するには、Visual Studio と WDK のセットアップ ファイルのパスを指定する必要があります。 これらのファイルを (インストールするのではなく) 保存してください。

1.  [Visual Studio Professional 2013](https://go.microsoft.com/fwlink/p/?linkid=316548) または [Visual Studio Ultimate 2013](https://go.microsoft.com/fwlink/p/?linkid=316520) をダウンロードします。 製品レイアウト (例: vs\_ultimate\_download.exe) をダウンロードします。 vs\_ultimate\_download.exe を実行するか保存するかを確認するメッセージが表示されたら、 **[実行]** をクリックしてダウンロード オプションを選び、ダウンロード パスとして **C:\\VSSetup** を指定します (後の手順が簡単になります)。 **[ダウンロード]** をクリックし、DVD レイアウトのローカル コピーをコンピューターにダウンロードしてインストールします。
2.  スタンドアロンの [SDK](https://go.microsoft.com/fwlink/p/?linkid=323507) をダウンロードします。 sdksetup.exe を実行するか保存するかを確認するメッセージが表示されたら、 **[実行]** をクリックし、ダウンロードの場所として **C:\\Kits\\SDK** を指定します。 **[次へ]** をクリックし、指示に従ってスタンドアロンの SDK をダウンロードします。
3.  [WDK 8.1](https://go.microsoft.com/fwlink/p/?linkid=317353) をダウンロードします。 wdksetup.exe を実行するか保存するかを確認するメッセージが表示されたら、 **[実行]** をクリックし、ダウンロードの場所として **C:\\Kits\\WDK** を指定します。 **[次へ]** をクリックし、指示に従って WDK をダウンロードします。 コンピューターに既に WDK がインストールされている場合は、コンピューターにインストールされている機能は最新であるというメッセージが Web インストール プログラムから表示されます。 ビルド環境に配置できるように WDK セットアップ ファイルをダウンロードするには、 **[次へ]** をクリックし、**C:\\Kits\\WDK** というパスを指定します。

## <a name="span-iddownloadscriptspanspan-iddownloadscriptspan2-download-the-buildlabsupport-files"></a><span id="download_script"></span><span id="DOWNLOAD_SCRIPT"></span>2.BuildLabSupport ファイルのダウンロード


ラボ内のコンピューターに WDK ビルド環境をインストールできるようにするには、まず、お使いのコンピューターにビルド ラボ サポート ファイルをダウンロードする必要があります。

1.  [BuildLabSupportfiles.zip](https://go.microsoft.com/fwlink/p/?linkid=321805) をダウンロードします。
2.  圧縮ファイルの内容をコンピューターに展開します。 展開されたファイルの中に BuildLabSupport ディレクトリがあり、必要なセットアップ ファイルとユーティリティが含まれています。

## <a name="span-idinstallscriptspanspan-idinstallscriptspan3-install-the-wdk81-build-environment"></a><span id="install_script"></span><span id="INSTALL_SCRIPT"></span>3.WDK 8.1 ビルド環境のインストール


ビルド ラボ サポート ファイルには、**setup.ps1** PowerShell コマンド ファイル含まれています。このコマンドは、必要な Visual Studio と WDK のコンポーネントを展開して、ターゲット ディレクトリ (フォルダー) にコピーします。 その後、このディレクトリを別の場所にコピーし、そこから、Visual Studio コマンド ライン インターフェイス (CLI) 開発環境でプロジェクトをビルドできます。

-   管理者特権のアクセス許可を使って ( **[管理者として実行]** ) コマンド プロンプト ウィンドウを開き、ビルド ラボ サポート ファイルを展開したディレクトリに移動します。 PowerShell コマンド スクリプト **setup.ps1** は、&lt;*root*&gt;\\BuildLabSupport ディレクトリにあります。

    PowerShell コマンドの構文は次のとおりです。

    <span codelanguage="PowerShell"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">PowerShell</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>powershell –executionpolicy bypass –file Setup.ps1 –DeployBuildLab –VSInstallerPath &lt;VSInstallerFilePath&gt; -KitInstallersPath &lt;KitInstallersPath&gt; -ExpansionRoot &lt;Target Directory&gt; –LogFilePath &lt;LogFilePath&gt; -CatalogFile &lt;Filename.xml&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    -   *&lt;VSInstallerFilePath&gt;* には、製品レイアウトを格納しているディレクトリと Visual Studio インストール プログラム (Vs\_ultimate.exe など) のパスを指定します。
    -   *&lt;KitInstallersPath&gt;* には、WDK と SDK のセットアップ ファイルのパスを指定します。
    -   *&lt;Target Directory&gt;* には、コンテンツの展開先となるターゲット ディレクトリを指定します。
    -   *&lt;LogFilePath&gt;* には、ログ ファイルの出力先を指定します。
    -   *&lt;Filename.xml&gt;* には、インストール中に展開される Microsoft Windows インストール ファイル (MSI) の一覧を含む CatalogFile の名前を指定します。 ファイルの名前は files.xml です。

    たとえば、次のコマンドでは、BuildLabSupport ディレクトリからスクリプトを実行し、C:\\BuildLabInstall ディレクトリにビルド環境をインストールします。

    ```cpp
    c:\BuildLabSupport>powershell -executionpolicy bypass -file Setup.ps1 -DeployBuildLab -VSInstallerPath c:\VSSetup -KitInstallersPath c:\Kits -E
    xpansionRoot C:\BuildLabInstall -CatalogFile  files.xml
    ```

## <a name="span-idbuildstepspanspan-idbuildstepspan4-build-windows-driver-projects-and-solutions"></a><span id="build_step"></span><span id="BUILD_STEP"></span>4.Windows ドライバー プロジェクトとソリューションのビルド


**ビルド環境のコマンド スクリプトを使う**

1.  コマンド プロンプト ウィンドウを開きます。 ターゲット ディレクトリ (C:\\BuildLabInstall など) にある LaunchBuildEnv.cmd ファイルを探します。
2.  **LaunchBuildEnv.cmd** を実行して、ビルド環境を起動します。
3.  MSBuild コマンドを使って、ドライバー プロジェクトとソリューションをビルドします。 次に、例を示します。

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj /p:Configuration="Win8.1 Debug" /p:Platform=Win32
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバーのビルド](building-a-driver.md)
* [MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)
 

 






