---
title: テンプレートを使ったユニバーサル Windows ドライバー (KMDF) の作成
description: このトピックでは、カーネルモード ドライバー フレームワーク (KMDF) を使ってユニバーサル Windows ドライバーを作成する方法について説明します。 Microsoft Visual Studio テンプレートを使って開始し、別のコンピューターにドライバーを展開してインストールします。
ms.assetid: 1E15A136-94BB-46C1-A438-9562C6BDCE7E
keywords:
- KMDF ドライバーの作成
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4afffd32b35b77560354b56e88d2a997394cbe9d
ms.sourcegitcommit: 20d98fc309319a0363b32510c9081b0d1775de93
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2019
ms.locfileid: "66840863"
---
# <a name="write-a-universal-windows-driver-kmdf-based-on-a-template"></a>テンプレートを使ったユニバーサル Windows ドライバー (KMDF) の作成

このトピックでは、カーネルモード ドライバー フレームワーク (KMDF) を使って[ユニバーサル Windows ドライバー](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)を作成する方法について説明します。 Microsoft Visual Studio テンプレートを使って開始し、別のコンピューターにドライバーを展開してインストールします。

最初に、[Microsoft Visual Studio 2015](https://go.microsoft.com/fwlink/p/?LinkId=698539) と [Windows Driver Kit (WDK) 10](https://go.microsoft.com/fwlink/p/?LinkId=733614) がインストールされていることを確認します。

[Debugging Tools for Windows](https://go.microsoft.com/fwlink/p?linkid=223405) は、WDK のインストールに含まれています。

## <a name="create-and-build-a-driver-package"></a>作成し、ドライバー パッケージのビルド

1. Microsoft Visual Studio を開きます。 **[ファイル]** メニューの **[新規] &gt; [プロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが次のように表示されます。
2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[WDF]** を選びます。
3. 中央のウィンドウで、 **[Kernel Mode Driver (KMDF)] (カーネル モード ドライバー (KMDF))** をクリックします。
4. **[名前]** フィールドに、プロジェクト名として「KmdfDriver」と入力します。

    > [!NOTE]
    > 新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。  

5. **[場所]** フィールドに、新規プロジェクトを作るディレクトリを入力します。
6. **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。 **[OK]** をクリックします。

    ![[新規プロジェクト] ダイアログ ボックスのスクリーン ショット (WDF とカーネル モード ドライバーが選ばれた状態)](images/vs2015-kmdf-new-project.png)

    Visual Studio により、1 つのプロジェクトと 1 つのソリューションが作られます。 これらは、次に示すように、 **[ソリューション エクスプローラー]** ウィンドウに表示されます ( **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** メニューの **[ソリューション エクスプローラー]** を選びます)。ソリューションには、UmdfDriver という名前のドライバー プロジェクトがあります。 ドライバーのソース コードを表示するには、 **[ソース ファイル]** の下に表示されるいずれかのファイルを開きます。 Driver.c と Device.c は手始めとして利用できるファイルです。

    ![[ソリューション エクスプローラー] のスクリーン ショット (ドライバー プロジェクトとパッケージ プロジェクトの各ファイルを表示した状態)](images/vs2015-kmdf-solution-explorer.png)

7. **[ソリューション エクスプローラー]** ウィンドウで、 **[ソリューション 'KmdfDriver' (1 件のプロジェクト)]** を右クリックし **[構成マネージャー]** をクリックします。 ドライバー プロジェクトとパッケージ プロジェクトの両方に対する構成とプラットフォームを選びます。 この作業では、Debug と x64 を選びます。

8. ドライバーをビルドし、ドライバー パッケージを作るには、 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 Visual Studio の **[出力]** ウィンドウにビルドの進行状況が表示されます ( **[出力]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[出力]** をクリックします)。

    ソリューションのビルドが成功したことを確認したら、Visual Studio を閉じることができます。

9. ビルドされたドライバーを確認するには、エクスプローラーで **[KmdfDriver]** フォルダーに移動し、**x64\\Debug\\KmdfDriver** に移動します。 フォルダーには以下が含まれています。

    * KmdfDriver.sys -- カーネル モード ドライバー ファイル
    * KmdfDriver.inf -- ドライバーをインストールするときに Windows で使われる情報ファイル

## <a name="deploy-the-driver"></a>ドライバーを展開します。

通常、ドライバーのテストと展開には、デバッガーとドライバーがそれぞれ別のコンピューター上で実行されます。 デバッガーを実行するコンピューターを*ホスト コンピューター*、ドライバーを実行するコンピューターを*ターゲット コンピューター*と呼びます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。 ドライバーのデバッグについて詳しくは、[Debugging Tools for Windows に関するページ](https://go.microsoft.com/fwlink/p?linkid=223405)をご覧ください。

ここまでは、ホスト コンピューター上の Visual Studio を使ってドライバーのビルドを行いました。 次にターゲット コンピューターの構成が必要です。

1. 「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](provision-a-target-computer-wdk-8-1.md)」の手順に従ってください。

    > [!TIP]
    > 手順に従って、ネットワーク ケーブルを使用して自動的に対象のコンピューターをプロビジョニングする場合は、ポートとキーを書き留めます。 デバッグの手順の後半でそれを使用します。 この例では、ポートに **50000**、キーに **1.2.3.4** を使用します。
    >
    > 実際のドライバー デバッグのシナリオでは、KDNET で生成されたキーを使用することをお勧めします。 KDNET を使用してランダム キーを生成する方法の詳細については、[ドライバーのデバッグ - ステップ バイ ステップ ラボ (Sysvad カーネル モード)](../debugger/debug-universal-drivers--kernel-mode-.md)のトピックを参照してください。

2. ホスト コンピューター上で、Visual Studio でソリューションを開きます。 ソリューション ファイル (KmdfDriver フォルダーの KmdfDriver.sln) をダブルクリックすることもできます。
3. **[ソリューション エクスプローラー]** ウィンドウで、 **[KmdfDriver]** プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
4. **[KmdfDriver Package のプロパティ ページ]** ウィンドウの左側のウィンドウで、 **[構成プロパティ] &gt; [Driver Install (ドライバーのインストール)] &gt; [配置]** の順にクリックします。
5. **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
6. **[リモート コンピューター名]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。 この作業では、MyTestComputer というコンピューターを使います。
7. **[Hardware ID Driver Update (ハードウェア ID のドライバーの更新)]** をクリックして、ドライバーのハードウェア ID を入力します。 この作業のハードウェア ID は Root\\KmdfDriver です。 **[OK]** をクリックします。

    ![[KmdfDriver Package プロパティ ページ] ウィンドウのスクリーン ショット ([ドライバーのインストール] と [展開] がクリックされた状態)](images/vs2015-kmdfdriver-property-pages.png)

    > [!NOTE]
    > この作業のハードウェア ID は特定のハードウェアを識別するものではありません。 [デバイス ツリー](https://go.microsoft.com/fwlink/p?linkid=399236)上でルート ノードの子として設定される架空のデバイスを表します。 実際のハードウェアについては、 **[Hardware ID Driver Update] (ハードウェア ID のドライバーの更新)** ではなく、 **[Install and Verify] (インストールと確認)** をクリックします。 ハードウェア ID は、ドライバーの情報ファイル (INF) に記載されています。 **[ソリューション エクスプローラー]** ウィンドウで **[KmdfDriver] &gt; [Driver Files (ドライバー ファイル)]** の順にクリックし、KmdfDriver.inf をダブルクリックします。 ハードウェア ID は \[Standard.NT$ARCH$\] の下にあります。

    ```C++
    [Standard.NT$ARCH$]
    %KmdfDriver.DeviceDesc%=KmdfDriver_Device, Root\KmdfDriver
    ```

8. **[ビルド]** メニューで、 **[ソリューションの配置]** を選択します。 Visual Studio は、ドライバーのインストールと実行に必要なファイルを対象のコンピューターに自動的にコピーします。 この処理には 1 ～ 2 分かかる可能性があります。

    ドライバーを展開すると、テスト コンピューターの %Systemdrive%\drivertest\drivers フォルダーにドライバー ファイルがコピーされます。 展開中に何か異変に気付いた場合は、テスト コンピューターにファイルがコピーされているかどうかを確認してください。 .inf、.cat、test cert、.sys など、必要なファイルがすべて %systemdrive%\drivertest\drivers フォルダーに存在することを確認します。

    ドライバーの展開の詳細については、「[テスト コンピューターへのドライバーの展開](../develop/deploying-a-driver-to-a-test-computer.md)」を参照してください。

## <a name="install-the-driver"></a>ドライバーのインストール

対象のコンピューターに KMDF ドライバーが展開されたので、次にドライバーをインストールします。 以前に Visual Studio で*自動*オプションを使用して対象のコンピューターをプロビジョニングした場合は、Visual Studio が対象のコンピューターがテスト署名されたドライバーをプロビジョニング プロセスの一部として実行するように設定します。 ここでは、DevCon ツールを使用してドライバーをインストールするだけです。

1. ホスト コンピューターで WDK インストール内の Tools フォルダーに移動し、DevCon ツールを見つけます。 たとえば、次のフォルダーを探します。

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

    DevCon ツールをリモート コンピューターにコピーします。

2. 対象のコンピューターでは、ドライバー ファイルを含むフォルダーに移動し、DevCon ツールを実行してドライバーをインストールします。
    1. ここで示しているのは、ドライバーのインストールに使う devcon ツールの一般的な構文です。

        *devcon install \<INF ファイル\> \<ハードウェア ID\>*

        このドライバーのインストールに必要な INF ファイルは KmdfDriver.inf です。 この INF ファイルには、ドライバーのバイナリ *KmdfDriver.sys* のインストールに必要なハードウェア ID が含まれています。 INF ファイルにあるハードウェア ID は **Root\\KmdfDriver** であることを思い出してください。
    2. 管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバー パッケージのフォルダーに移動し、次のコマンドを入力します。

        **devcon install kmdfdriver.inf root\\kmdfdriver**

        *devcon* が認識されないというエラー メッセージが表示された場合は、*devcon* ツールへのパスを追加してみてください。 たとえば、対象のコンピューター上の *C:\\Tools* という名前のフォルダーにコピーする場合は、次のコマンドを使ってみます。

        **c:\\tools\\devcon install kmdfdriver.inf root\kmdfdriver**

        ダイアログ ボックスには、テスト ドライバーが署名されていないドライバーであることが示されます。 **[かまわず続行]** をクリックして続行します。

        ![ドライバーのインストールに関する警告のスクリーン ショット](../debugger/images/debuglab-image-install-security-warning.png)

## <a name="debug-the-driver"></a>ドライバーのデバッグ

対象のコンピューターに KMDF ドライバーをインストールしたので、ホスト コンピューターからリモートでデバッガーをアタッチします。

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 WinDbg.exe ディレクトリに移動します。 Windows キットの一部としてインストールされた Windows Driver Kit (WDK) に含まれる WinDbg.exe の x64 バージョンを使います。 WinDbg.exe の既定のパスを次に示します。

    *C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64*

2. 次のコマンドを使用して、対象のコンピューターで WinDbg を起動してカーネル デバッグ セッションに接続します。 ポートとキーの値は、対象のコンピューターをプロビジョニングするために使用したものと同じである必要があります。 ポートに **50000**、キーに **1.2.3.4** を使用します。これは展開の手順で使用した値です。 *k* フラグは、これがカーネル デバッグ セッションであることを示します。

    **WinDbg -k net:port=50000,key=1.2.3.4**

3. **[デバッグ]** メニューの **[中断]** をクリックします。 ホスト コンピューター上のデバッガーが、ターゲット コンピューターに割り込みます。 **デバッガーのコマンド** ウィンドウに、カーネルのデバッグ コマンド プロンプト **kd\>** が表示されます。

4. この段階で、**kd&gt;** プロンプトに対してコマンドを入力することにより、デバッガーの操作を試してみることができます。 たとえば、次のようなコマンドを試すことができます。

    * [lm](https://go.microsoft.com/fwlink/p?linkid=399236)
    * [.sympath](https://go.microsoft.com/fwlink/p?linkid=399238)
    * [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)
    * [x KmdfHelloWorld!\*](https://go.microsoft.com/fwlink/p?linkid=399240)

5. 対象のコンピューターを再び実行するには、 **[デバッグ]** メニューの **[続行]** をクリックするか、または "g" を押してから、Enter キーを押します。
6. デバッグ セッションを停止するには、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。

    > [!IMPORTANT]
    > "go" コマンドを使用して、デバッガーを終了する前に対象のコンピューターをもう一度実行するようにしてください。そうしないと、対象のコンピューターがまだデバッガーとやり取りをしている状態であるため、マウスとキーボード入力に応答しないままになります。

ドライバー デバッグ プロセスの詳細な手順については、「[ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)」を参照してください。

リモート デバッグの詳細については、「[WinDbg を使用したリモート デバッグ](../debugger/remode-debugging-using-windbg.md)」を参照してください。

## <a name="using-the-driver-module-framework-dmf"></a>ドライバー モジュール フレームワーク (DMF) を使用します。

[ドライバー モジュール フレームワーク (DMF)](https://github.com/Microsoft/DMF) WDF WDF ドライバー開発者向けの特別な機能を有効にする拡張機能です。 これにより、開発者が適切かつ迅速に WDF ドライバーの作成が役立ちます。

DMF のフレームワーク WDF オブジェクトの作成を許可する DMF モジュールと呼ばれます。 DMF のこれらのモジュールのコードは、さまざまなドライバーの間で共有できます。 さらに、DMF のバンドル、ドライバーと外観を開発しました DMF モジュールのライブラリは値を指定を他のドライバー開発者。

DMF には、WDF は置換されません。 DMF は、WDF で使用される 2 つ目のフレームワークです。 DMF を引き続き利用する開発者では、WDF とそのすべてのプリミティブを使用してデバイス ドライバーを書き込みます。

詳細については、次を参照してください。[ドライバー モジュール フレームワーク (DMF)](https://github.com/Microsoft/DMF)します。

## <a name="related-topics"></a>関連トピック

[ドライバーの開発、テスト、および展開](https://go.microsoft.com/fwlink/p?linkid=399234)

[Windows 用デバッグ ツール](https://go.microsoft.com/fwlink/p?linkid=223405)

[ユニバーサル ドライバーのデバッグ - ステップ バイ ステップ ラボ (Echo カーネル モード)](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)

[初めてのドライバーの作成](writing-your-first-driver.md)
