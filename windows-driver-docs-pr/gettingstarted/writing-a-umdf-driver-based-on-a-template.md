---
title: テンプレートを使ったユニバーサル Windows ドライバー (UMDF 2) の作成
description: このトピックでは、ユーザーモード ドライバー フレームワーク (UMDF) 2 を使ってユニバーサル Windows ドライバーを作成する方法について説明します。 Microsoft Visual Studio テンプレートを使って開始し、別のコンピューターにドライバーを展開してインストールします。
ms.assetid: 03A3E389-8350-4E4B-9345-E50DD425374D
keywords:
- UMDF ドライバーの作成
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22d87ddd88af414359d0f792cb4bc21987db7e4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359293"
---
# <a name="write-a-universal-windows-driver-umdf-2-based-on-a-template"></a>テンプレートを使ったユニバーサル Windows ドライバー (UMDF 2) の作成

このトピックでは、ユーザーモード ドライバー フレームワーク (UMDF) 2 を使って[ユニバーサル Windows ドライバー](https://docs.microsoft.com/windows-hardware/drivers)を作成する方法について説明します。 Microsoft Visual Studio テンプレートを使って開始し、別のコンピューターにドライバーを展開してインストールします。

最初に、最新バージョンの Microsoft Visual Studio と Windows Driver Kit (WDK) があることを確認します。 ダウンロード リンクについては、「[Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」をご覧ください。

[Debugging Tools for Windows](https://go.microsoft.com/fwlink/p?linkid=223405) は、WDK のインストールに含まれています。

## <a name="create-and-build-a-driver"></a>ドライバーの作成とビルド

>[!NOTE]
>新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。

1. Visual Studio を開きます。 **[ファイル]** メニューの **[新規] &gt; [プロジェクト]** をクリックします。
2. [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[Visual C++] &gt; [Windows ドライバー] &gt; [WDF]** の順に移動します。 **[User Mode Driver (UMDF V2) (ユーザー モード ドライバー (UMDF V2))]** を選びます。
3. **[名前]** フィールドに、プロジェクト名として「UmdfDriver」と入力します。
4. **[場所]** フィールドに、新規プロジェクトを作るディレクトリを入力します。
5. **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。 **[OK]** をクリックします。

    ![[新規プロジェクト] ダイアログ ボックスのスクリーン ショット (WDF とユーザー モード ドライバーが選ばれた状態) ](images/vs2015-umdf2-template.png)

    Visual Studio により、1 つのプロジェクトと 1 つのソリューションが作られます。 これらは、 **[ソリューション エクスプローラー]** ウィンドウに表示されます ( **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** メニューの **[ソリューション エクスプローラー]** を選びます)。ソリューションには、UmdfDriver という名前のドライバー プロジェクトがあります。 ドライバーのソース コードを表示するには、 **[ソース ファイル]** の下に表示されるいずれかのファイルを開きます。 Driver.c と Device.c は手始めとして利用できるファイルです。

    ![[ソリューション エクスプローラー] のスクリーン ショット (ドライバー プロジェクトの各ファイルを表示した状態)](images/vs2015-umdf2-solution-explorer.png)

6. **[ソリューション エクスプローラー]** ウィンドウで、 **[ソリューション 'UmdfDriver' (1 件のプロジェクト)]** を右クリックし **[構成マネージャー]** をクリックします。 ドライバー プロジェクトに対する構成とプラットフォームを選びます。 たとえば、**Debug** と **x64** を選びます。
7. **[ソリューション エクスプローラー]** ウィンドウで、 **[UmdfDriver]** を右クリックして、 **[プロパティ]** をクリックします。 **[構成プロパティ] &gt; [Driver Settings (ドライバーの設定)] &gt; [全般]** の順に移動し、 **[ターゲット プラットフォーム]** が既定で **[ユニバーサル]** に設定されていることを確認します。
8. ドライバーをビルドするには、 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。 Microsoft Visual Studio の **[出力]** ウィンドウにビルドの進行状況が表示されます ( **[出力]** ウィンドウが表示されていない場合は、 **[表示]** メニューの **[出力]** をクリックします)。

    ビルド出力に "" が含まれていることを確認します。

    ``` syntax
    >  Driver is a Universal Driver.
    ```

    ソリューションのビルドが成功したことを確認したら、Visual Studio を閉じることができます。

9. ビルドされたドライバーを確認するには、エクスプローラーで **[UmdfDriver]** フォルダーに移動し、**x64\\Debug\\UmdfDriver** に移動します。 ディレクトリには次のファイルが含まれています。

    * UmdfDriver.dll -- ユーザー モード ドライバー ファイル
    * UmdfDriver.inf -- ドライバーをインストールするときに Windows で使われる情報ファイル

## <a name="deploy-and-install-the-universal-windows-driver"></a>ユニバーサル Windows ドライバーの展開とインストール

通常、ドライバーのテストと展開には、デバッガーとドライバーがそれぞれ別のコンピューター上で実行されます。 デバッガーを実行するコンピューターを*ホスト コンピューター*、ドライバーを実行するコンピューターを*ターゲット コンピューター*と呼びます。 ターゲット コンピューターは*テスト コンピューター*とも呼ばれます。

ここまでは、ホスト コンピューター上の Visual Studio を使ってドライバーのビルドを行いました。 次にターゲット コンピューターの構成が必要です。 「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 10)](provision-a-target-computer-wdk-8-1.md)」の手順に従ってください。 その後で、ドライバーの展開、インストール、読み込み、デバッグを行うための準備をします。

1. ホスト コンピューター上で、Visual Studio でソリューションを開きます。 ソリューション ファイル (UmdfDriver フォルダーの UmdfDriver.sln) をダブルクリックすることもできます。
2. **[ソリューション エクスプローラー]** ウィンドウで、 **[UmdfDriver]** を右クリックして、 **[プロパティ]** をクリックします。
3. 次に示すように、 **[UmdfDriver のプロパティ ページ]** ウィンドウで、 **[構成プロパティ] &gt; [Driver Install (ドライバーのインストール)] &gt; [配置]** の順に移動します。
4. **[展開前にドライバーの以前のバージョンを削除する]** チェック ボックスをオンにします。
5. **[Target Device Name (ターゲット デバイス名)]** については、テストとデバッグ用に構成したコンピューターの名前を選んでください。
6. **[Hardware ID Driver Update (ハードウェア ID のドライバーの更新)]** をクリックして、ドライバーのハードウェア ID を入力します。 この作業のハードウェア ID は Root\\UmdfDriver です。 **[OK]** をクリックします。

    ![[UmdfDriver のプロパティ ページ] のスクリーン ショット ([ドライバーのインストール] と [配置] がクリックされた状態)](images/vs2015-deploy.png)

    **注**  この作業のハードウェア ID は特定のハードウェアを識別するものではありません。 [デバイス ツリー](https://go.microsoft.com/fwlink/p?linkid=399236)上でルート ノードの子として設定される架空のデバイスを表します。 実際のハードウェアについては、 **[Hardware ID Driver Update] (ハードウェア ID のドライバーの更新)** ではなく、 **[Install and Verify] (インストールと確認)** をクリックします。
    ハードウェア ID は、ドライバーの情報ファイル (INF) に記載されています。 **[ソリューション エクスプローラー]** ウィンドウで **[UmdfDriver] &gt; [Driver Files (ドライバー ファイル)]** の順にクリックし、UmdfDriver.inf をダブルクリックします。 ハードウェア ID は \[Standard.NT$ARCH$\] の下に記載されています。

    ```ManagedCPlusPlus
    [Standard.NT$ARCH$]
    %DeviceName%=MyDevice_Install,Root\UmdfDriver
    ```

7. **[デバッグ]** メニューの **[デバッグ開始]** をクリックするか、キーボードで **F5** キーを押します。
8. ドライバーがターゲット コンピューターに展開、インストールされ、読み込まれるまで待機します。 数分かかる場合があります。

## <a name="using-the-driver-module-framework-dmf"></a>Driver Module Framework (DMF) の使用

[Driver Module Framework (DMF)](https://github.com/Microsoft/DMF) は、WDF ドライバー開発者向けの追加機能が有効になる WDF の拡張機能です。 開発者は、どのような種類の WDF ドライバーでも適切にに短時間で作成できるようになります。

フレームワークとしての DMF によって、DMF モジュールという WDF オブジェクトを作成できます。 これらの DMF モジュールのコードは、異なるドライバー間で共有できます。 さらに、DMF は、ドライバー用に開発された DMF モジュールのライブラリをバンドルしており、他のドライバー開発者にも役立ちます。

DMF は WDF に置き換わるものではありません。 DMF は WDF と共に使用される 2 つ目のフレームワークです。 DMF を利用している開発者は引き続き WDF とそのすべてのプリミティブを使用してデバイス ドライバーを作成します。

詳細については、[Driver Module Framework (DMF)](https://github.com/Microsoft/DMF)を参照してください。

## <a name="related-topics"></a>関連トピック

[ドライバーの開発、テスト、および展開](https://go.microsoft.com/fwlink/p?linkid=399234)

[Windows 用デバッグ ツール](https://go.microsoft.com/fwlink/p?linkid=223405)

[初めてのドライバーの作成](writing-your-first-driver.md)
