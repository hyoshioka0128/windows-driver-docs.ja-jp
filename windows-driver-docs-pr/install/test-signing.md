---
title: テスト署名
description: Windows 64 ビット版には、ドライバーに読み込まれるためにデジタル署名などのカーネル モードで実行されているすべてのソフトウェアが必要です。
ms.assetid: 52F309E4-9553-456B-BBD6-217318FC7222
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a76b55ed3084b756e802d834f071e57629e63b8d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349997"
---
# <a name="test-signing"></a>テスト署名


Windows Vista 以降では、x64 ベース バージョンの Windows には、ドライバーに読み込まれるためにデジタル署名などのカーネル モードで実行されているすべてのソフトウェアが必要です。 最初に、ドライバーの有効な署名を要求する場合の読み込み時の実施を一時的に無効にする (各起動時に、Windows の読み込み前に) F8 スイッチを使用できます。 最初のいくつかの使用後面倒なこのなります。 適切な BCDEdit のコマンドを使用した後、同じ負荷時の強制チェックを無効になりますテスト コンピューターにカーネル デバッガーをアタッチすることができます。 ただし、最終的には必要になるテストへの署名をドライバーの開発、および最終的にリリース署名中にユーザーに公開する前に、ドライバー。

## <a name="installing-an-unsigned-driver-during-development-and-test"></a>開発中およびテスト中の署名されていないドライバーのインストール


*抜粋*[開発およびテスト中に、署名されていないドライバーをインストールする](installing-an-unsigned-driver-during-development-and-test.md):

既定では、64 ビット バージョンの Windows Vista と Windows の以降のバージョンがカーネル モードのドライバーの読み込み、カーネルがドライバーの署名を検証できる場合にのみ。 ただし、初期のドライバーの開発中、およびテスト自動化されていないにこの既定の動作を無効にできます。 開発者は、一時的に有効なドライバーの署名の読み込み時の強制を無効にするのに、次のメカニズムのいずれかを使用できます。 ただし、プラグ アンド プレイ (PnP) がインストールされているドライバーのテストを完全に自動化、[カタログ ファイル](catalog-files.md)のドライバーを署名する必要があります。 Windows Vista および Windows の以降のバージョンの表示、ドライバーの署名されていないドライバーをドライバーのインストールを承認するためにシステム管理者を必要とする ダイアログ ボックスの署名、せず、すべてのユーザーができない可能性があるため、ドライバーの署名が必要です、ドライバーをインストールして、デバイスを使用してから必要な権限。 Windows Vista および Windows の以降のバージョンでは、この PnP ドライバー インストールの動作を無効にできません。

### <a name="use-the-f8-advanced-boot-option"></a>**F8 の 詳細ブート オプションを使用して、**

Windows Vista および以降のバージョンの Windows F8 高度なブート オプション サポート--「を無効にするドライバー署名の強制」--をカーネル モード ドライバー用のシステムの現在のセッションでのみの読み込み時の署名の強制を無効にします。 この設定は、システムの再起動後は保持されません。

署名の強制、ドライバーを無効にするオプションを提供する再起動中に、次のブート オプション画面が表示されます。 このプロビジョニングでは、テスト目的で未署名のドライバのインストールを許可します。

![f8 の 詳細ブート オプションを示すスクリーン ショット](images/tutorialf8.png)

### <a href="" id="attach-a-kernel-debugger-to-disable-signature-verification"></a> 署名の検証を無効にするカーネル デバッガーをアタッチします。

開発またはテスト コンピューターに、アクティブなカーネル デバッガーをアタッチすると、カーネル モード ドライバーの読み込み時の署名の強制が無効にします。 このデバッグ構成を使用するには、開発、デバッグのコンピューターを接続またはコンピューターのテストしカーネルの開発でのデバッグを有効にすることもコンピューターをテストするには、次のコマンドを実行します。

```cpp
bcdedit -debug on
```

BCDEdit を使用して、ユーザーは、システムの Administrators グループのメンバーであるし、管理者特権のコマンド プロンプトからコマンドを実行する必要があります。 管理者特権のコマンド プロンプト ウィンドウを開くには、デスクトップ ショートカットを作成*Cmd.exe*、ショートカットを右クリックし、選択、**管理者として実行**します。

ただし、状況を開発者が、カーネル デバッガーをアタッチする必要があるまだ読み込み時の署名の強制を維持する必要もありますがもあります。 参照してください[付録 1。カーネル デバッグ モードのカーネル モードの署名の検証を適用する](appendix-1--enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode.md)これを実現する方法について。

## <a name="test-sign-a-driver-package"></a>テスト署名ドライバー パッケージ


ドライバー署名の強制要件をバイパスする上記の 2 つのメソッドを使用する代わりには、最適な方法は、サインオン ドライバー パッケージをテストします。 開発用コンピューターでは、テスト署名とドライバーのインストールを実行できますが、2 つのコンピューターが存在することも、開発し、署名、およびその他のテスト用に 1 つ。

*抜粋*[テスト署名ドライバー パッケージ方法](how-to-test-sign-a-driver-package.md):

<a href="" id="signing-computer"></a>**コンピューターの署名**  
これは、テスト署名ドライバーが Windows Vista および Windows の以降のバージョンのパッケージ化するために使用するコンピューターです。 このコンピューターでは、Windows XP SP2 または以降のバージョンの Windows が実行されている必要があります。 使用するには、[ドライバーの署名ツール](https://msdn.microsoft.com/library/windows/hardware/ff552958)以降のバージョンの Windows Driver Kit (WDK) がインストールされている、このコンピューターは、Windows Vista をいる必要があります。 これにより、開発用コンピューターこともできます。

<a href="" id="test-computer"></a>**テスト コンピューター**  
これは、インストールし、テスト署名されたドライバー パッケージをテストするために使用するコンピューターです。 このコンピューターでは、Windows Vista または Windows の以降のバージョンが実行されている必要があります。

## <a name="test-signing-procedure"></a>署名のプロシージャをテストします。


ドライバー パッケージは、バイナリ、ドライバー、INF ファイル、CAT ファイルおよびその他の必要なファイルが格納されます。 ターゲット プロセッサの種類を 1 つ以上のドライバーが組み込まれている場合、ドライバー パッケージは x86、AMD64、IA64 などのサブディレクトリを含めることができます。 開発/署名のコンピューターを使用してこれらの手順を実行します。

次の手順では、サインオン ドライバー パッケージをテストする手順について説明します。

1.  ターゲットのドライバーをビルドします。 Windows 8.0 または Windows 8.1 では、ドライバーの構築は、対応する WDK で Visual Studio 2012 または Visual Studio 2013 を使用した場合、インストールされているなど、Windows 8.0 または WDK 8.1 それぞれします。

    Visual Studio 2012 または Visual Studio 2013 の対応するツール/ビルド コマンド ウィンドウからは、以下に示すすべてのコマンド ツールを使用してください。

    **注**for Visual Studio のコマンド ツールが c: のインストール ディレクトリにある\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\ツール\\ショートカット




コマンド プロンプトの 5 つのショートカットのいずれかが、makecert.exe、inf2cat.exe、signtool.exe、certmgr.exe をなど、コマンド。

一般的な"開発者コマンド プロンプト for VS2013"ことができます。 ショートカットは、アクセスしやすいように、タスク バーをにピン留めできます。

**注**注意: Visual Studio を使用してドライバーの署名のコマンド ツール アプローチではなく使用することできますも Visual Studio 2013 開発環境 (IDE とも呼ばれる) ドライバー パッケージに署名します。 参照してください[付録 2。Visual Studio を使用したドライバーの署名](appendix-2--signing-drivers-with-visual-studio.md)詳細についてはします。




2.  ドライバー パッケージ フォルダーを作成し、任意のサブディレクトリに必要な例 c: を維持、ドライバー ファイルをコピー\\DriverTestPackage します。
3.  ドライバー パッケージの inf ファイルを作成します。 Inf ファイルの日付でない 08/21/2006 Vista と同様に Windows 8.0、Windows 8.1、Windows 7.0、Windows 7.1 の後の日付の前に確認します。 エラーは報告されませんように inf ファイルで WDK から chkinf.bat ツールを使用して inf ファイルをテストすることをお勧めします。 プリンター ドライバーである場合は、ツール chkinf.bat と WDK から INFGate.exe inf ファイルをテストします。
4.  *抜粋*[テスト証明書を作成する](creating-test-certificates.md):

    次のコマンドラインの例では、MakeCert を使用して、次のタスクを完了します。

    -   という名前のテスト用の自己署名証明書作成*Contoso.com(Test)* します。 この証明書は、同じサブジェクト名と証明書機関 (CA) の名前を使用します。

    -   という名前の出力ファイルに証明書のコピーを配置*ContosoTest.cer*します。

    -   という名前の証明書ストア、証明書のコピーを配置*PrivateCertStore*します。 テスト証明書を配置する*PrivateCertStore*可能性がある場合、システムの他の証明書から独立した状態に保ちます。

    次の MakeCert コマンドを使用して作成する、 *Contoso.com(Test)* 証明書。

    ```cpp
    makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) ContosoTest.cer
    ```

    各項目の意味は次のとおりです。

    -   **-R**オプションは、発行者とサブジェクトの同じ名前の自己署名証明書を作成します。

    -   **-Pe**オプションは、証明書に関連付けられている秘密キーをエクスポートすることを指定します。

    -   **-Ss**オプションは、テスト証明書を含む証明書ストアの名前を指定します (*PrivateCertStore*)。

    -   **-N CN =** オプション Contoso.com(Test)、証明書の名前を指定します。 この名前を併用、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)証明書を識別するためのツール。

    -   *ContosoTest.cer* Contoso.com(Test) テストの証明書のコピーを含むファイルの名前です。 証明書ファイルを使用して、信頼されたルート証明機関証明書ストアと信頼された発行元の証明書ストアに証明書を追加します。

    *抜粋*[テスト証明書の表示](viewing-test-certificates.md):

    証明書が作成され、コピーは、証明書ストアに、Microsoft 管理コンソール (MMC) の証明書スナップインで使用できますそれを表示します。 MMC で証明書を表示するには、次の操作を行います**証明書**スナップイン。

    1.  クリックして**開始**し、[検索の開始] をクリックします。

    2.  証明書スナップインを開始する入力 Certmgr.msc とキーを押して、 **Enter**キー。

    3.  証明書スナップインの左側のウィンドウで、PrivateCertStore 証明書ストアのフォルダーを展開し、証明書をダブルクリックします。

    次のスクリーン ショットの証明書スナップインでビューを示しています、 **PrivateCertStore**証明書ストアのフォルダー。

    ![テスト証明書を示す証明書ストアのスクリーン ショット ](images/tutorialprivatecertstore.png)

    Contoso.com(Test) 証明書に関する詳細を表示するには、右側のウィンドウで、証明書をダブルクリックします。 次のスクリーン ショットでは、証明書に関する詳細を表示します。

    ![contoso.com の全般的な情報を表示する証明書 ウィンドウのスクリーン ショットは証明書を (テスト)](images/tutorialcertificategeneraltab.png)

    証明書のダイアログ ボックスを示すことに注意してください。"この CA ルート証明書は信頼されていません。 信頼を有効にするには、この証明書をインストール、信頼されたルート証明機関ストア内。" これは、想定される動作です。 Windows が既定では、"Contoso.com(Test)"証明機関を信頼しないために、証明書を検証できません。

5.  カタログ ファイル (拡張子は .cat) を作成します。 次に示す inf2cat ツールを使用して、カタログ ファイルを作成します。 スペースが許可されないこと、スイッチの/driver に注意してください:&lt;領域がありません&gt;&lt;の完全なパス&gt;、/os::&lt;スペース&gt;&lt;os1 名前&gt;、:&lt;領域がありません&gt;&lt;os2 名前&gt;します。

    ```cpp
    inf2cat  /v  /driver:C:\DriverTestPackage  /os:7_64,7_x86 ,XP_X86
    ```

    これにより、ドライバーの .inf ファイルで指定された名前のカタログ ファイルが作成されます。 追加のコンマ区切りの Os を選択的に追加できる、またはすべてスペースを含めずに次のようです。

    ```cpp
    /os:2000,XP_X86,XP_X64,Server2003_X64,Vista_X64,Vista_X86,7_x86,7_64,Server2008_x86,Server2008_x64,Sever2008_IA64,Server2008R2_x86,Server2008R2_x64,Server2008R2_IA64,8_x86,8_x64, 8_ARM, Server8_x64
    ```

    新しい 8.1 WDK から更新された inf2cat には、6_3_X86、6_3_X64、6_3_ARM および SERVER_6_3_X64 の/os オプションの値があります。

    バージョン セクションの INF ファイルの例です。

    ```cpp
    [Version]
    Signature="$WINDOWS NT$"
    Class=TOASTER
    ClassGuid={B85B7C50-6A01-11d2-B841-00C04FAD5171}
    Provider=%ToastRUs%
    DriverVer=09/21/2006,6.0.5736.1
    CatalogFile.NTx86  = tostx86.cat
    CatalogFile.NTIA64 = tostia64.cat
    CatalogFile.NTAMD64 = tstamd64.cat
    ```

    /Driver (または/drv) オプションでは、1 つまたは複数の INF ファイルを含むディレクトリを指定します。 このディレクトリ内でそれらの INF ファイルを 1 つまたは複数の CatalogFile ディレクティブを含むカタログ ファイルが作成されます。 カタログのファイル名では、8.3 形式の名前に制限されません。

    コマンドライン引数/os:7_X64 が使用されている場合、Inf2Cat はカタログ ファイルの tstamd64.cat を作成します。 同様に、ツールは、/os:XP_X86、オプションを使用する場合、同様に Server2008R2_IA64 のカタログ ファイルの toastx86.cat を作成します。 1 つだけカタログ ファイルが必要な場合、次に示すように、INF ファイルにエントリを 1 つだけで十分です。

    ```cpp
    CatalogFile.NT  = toaster.cat
    ```

    または

    ```cpp
    CatalogFile = toaster.cat
    ```

    INF ファイルで日付がない場合、OS のリリース日よりも大きい/os パラメーターで Windows 7 では、INF ファイルで設定した日付が過去の日付の場合、inf2cat ツールによって、次のエラーを報告されます。

    ```cpp
    Signability test failed.
    Errors:
    22.9.7: DriverVer set to incorrect date (must be postdated to 4/21/2009 for newest OS) in \toaster.inf
    ```

    Inf2cat ツールは、各フォルダーとサブフォルダー INF ファイルにエントリを持つすべてのファイルの存在についての非常に厳格です。 このような不足しているエントリの意味のあるエラー メッセージがあります。

    Cat ファイルは、二重 をクリックまたはファイルを右クリックして、およびオープンを選択してエクスプ ローラーから開くことができます。 [セキュリティ] タブは、GUID 値を持つエントリをいくつか紹介します。 GUID 値を選択すると、ドライバー パッケージのドライバー ファイルを含む詳細が表示され、Os が次に示すように追加します。

    ```cpp
    OSAttr  2:5.1,6.1
    ```

    数 5.1 は、XP OS のバージョン番号と Windows 7.0 OS は 6.1 です。

    選択した Os およびドライバー ファイルを含めることを確認する cat ファイルをチェックすることをお勧めします。 いつでも場合、ドライバー ファイルが追加または削除、INF ファイルが変更された、cat ファイルを再作成され再度署名する必要があります。 任意の省略は、ここでは、セットアップ ログ ファイル (Vista 以降の setupapi.dev.log または xp setupapi.log ファイル) に報告されますインストール エラーが発生します。

6.  *抜粋*[テスト署名ドライバー パッケージのカタログ ファイル](test-signing-a-driver-package-s-catalog-file.md):

    次のコマンドラインは、署名ツールは、次を実行する方法を示します。

    -   テスト署名、 *tstamd64.cat*のカタログ ファイル、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)します。 詳細についてはこの[カタログ ファイル](catalog-files.md)が作成されるを参照してください[ドライバー パッケージのテスト署名カタログ ファイルを作成する](creating-a-catalog-file-for-test-signing-a-driver-package.md)します。

    -   テスト署名、PrivateCertStore から Contoso.com(Test) 証明書を使用します。 この証明書の作成方法の詳細については、[テスト証明書を作成する](creating-test-certificates.md)を参照してください。

    -   タイム スタンプ機関 (TSA) 経由のデジタル署名のタイムスタンプ。

    テスト署名、 *tstamd64.cat*カタログ ファイルを次のコマンドラインを実行します。

    ```cpp
    Signtool sign /v /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
    ```

    各項目の意味は次のとおりです。

    -   **サインオン**コマンドは、指定したカタログ ファイルの署名に SignTool を構成します。 tstamd64.cat します。

    -   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

    -   **/S**オプションは、証明書ストアの名前を指定します (*PrivateCertStore)* テスト証明書を格納しています。

    -   **/N**オプションは、証明書の名前を指定します (*Contoso.com(Test))* 指定された証明書ストアにインストールされています。

    -   **/T**オプション、TSA の URL を指定します (*http://timestamp.verisign.com/scripts/timstamp.dll*) が、タイムスタンプ、デジタル署名します。
        **重要な**キーの失効がコード署名の秘密キーの署名者の場合は、侵害の必要な情報を提供するタイムスタンプを含むです。




-   *tstamd64.cat*デジタル署名されるカタログ ファイルの名前を指定します。

tstamd64.cat では、デジタル署名されるカタログ ファイルの名前を指定します。 前に、の説明に従って、cat ファイルを開くことができます。


7.  *変更された抜粋*[テスト署名ドライバーは、埋め込みの署名](test-signing-a-driver-through-an-embedded-signature.md):

    -   64 ビット バージョンの Windows Vista および Windows の以降のバージョンでは、埋め込みの署名がカーネル モード コード署名の要件に必要です。 これは、ドライバーのドライバー パッケージがデジタル署名済みカタログ ファイルを持つかどうかに関係なく必要です。

    記号のカーネル モード ドライバーのバイナリ ファイルを埋め込むには、コマンドを次に示します。

    ```cpp
    signtool sign  /v  /s  PrivateCertStore  /n  Contoso.com(Test)  /t http://timestamp.verisign.com/scripts/timestamp.dll   amd64\toaster.sys
    ```

    amd64\\toaster.sys を埋め込む署名されるカーネル モード バイナリ ファイルの名前を指定します。

    WDK 7.1 のインストール ディレクトリ内でトースター サンプルにある src\\全般\\トースター\\toastpkg\\toastcd\\ディレクトリ。 Windows 8 または 8.1 の WDK サンプルは、Microsoft ダウンロード サイトからダウンロードされるは。 サンプルは、Windows 8 または 8.1 の Windows Driver Kit に付属していません。

    カタログ ファイルをダブルクリックして Windows エクスプ ローラーでファイルを開いたときに、次のスクリーン ショットが表示されます。 「署名の表示」がここで強調表示されていることに注意してください。

    ![セキュリティ カタログ ファイルの一般的な情報を示すスクリーン ショット](images/tutorialsecuritycatalogfilegeneraltab.png)

    "署名の表示 をクリックすると、ダイアログ自体から証明書の表示"、「証明書のインストール」のオプションが、こうから、次へ の表示オプションを提供する以下のスクリーン ショットが表示されます。 ただし、certmgr.exe ツールを使用して証明書のインストールの推奨されるコマンド ライン オプションを提供しています。

    ![デジタル署名の詳細に関する一般的な情報を示すスクリーン ショット](images/tutorialdriversignaturedetails.png)

    ![証明書に関する一般的な情報を示すスクリーン ショット](images/tutorialcertificategeneraltab.png)

ドライバー署名のコンピューターまたはテスト コンピューターでテストできます。 テスト コンピューターを使用している場合は、ファイルの構造をそのまま維持するマシンにドライバー パッケージをコピーします。 ツールの certmgr.exe は、テスト コンピューターにコピーするのにもあります。 テスト コンピューターを使用する場合は、c: Toastpkg テスト署名されたドライバー パッケージをコピー\\トースター一時フォルダーです。

次の手順では、いずれかのマシンで使用してドライバーをテストする手順について説明します。

1.  管理者特権でコマンド ウィンドウで、次のコマンドを実行します。

    ```cpp
    bcdedit  /set  testsigning  on
    ```

    コンピューターを再起動します。

2.  *抜粋を選択した*[テスト コンピューターにテスト証明書をインストールするを使用して CertMgr](using-certmgr-to-install-test-certificates-on-a-test-computer.md):

    証明書のコピー (*.cer*) に使用したファイルは、[テスト署名](test-signing-driver-packages.md)ドライバーは、テスト コンピューターにします。 証明書ファイルは、テスト コンピューター上の任意のディレクトリにコピーできます。

    次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼されたルート証明機関。

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine root
    ```

    次の CertMgr コマンドでは、証明書のファイル、証明書を追加します。 *CertificateFileName.cer*テスト コンピューター上のストアの証明書には、信頼された発行元。

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
    ```

    場所 (*からの抜粋* [ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411))。

    /add CertificateName

    指定された証明書ファイルの証明書ストアに証明書を追加します。

    /s

    システム ストアに証明書ストアを指定します。

    /r RegistryLocation

    HKEY_LOCAL_MACHINE の下のシステム ストアのレジストリの場所を指定します。

    CertificateStore

    証明書ストア"localMachine root"の場合も同様の trustedpublisher を指定します。

    コンピューターを再起動します。 Certmgr.msc を実行し、上記の 2 つの場所、ContosoTest.cer が表示されていることを確認できます。 表示されない場合、証明書をインストールする別の方法を証明書を開いて、上記の 2 つのノードにインストールし、もう一度確認します。

3.  Cat ファイルと sys ファイルの署名を確認します。 管理者特権でコマンド ウィンドウを開き、cat、inf と sys ファイルがあるドライバー パッケージのディレクトリに移動して、signtool.exe は、コンピューターで利用できると仮定すると、します。 適切なディレクトリで次のコマンドを実行します。

    [カタログ ファイルの署名の SPC 検証](verifying-the-spc-signature-of-a-catalog-file.md):

    ```cpp
    signtool  verify  /v  /kp  /c  tstamd64.cat  toaster.inf
    ```

    埋め込みのサインインを確認するには、次のコマンドを実行します。

    [リリース署名されたドライバー ファイルの署名の検証](verifying-the-signature-of-a-release-signed-driver-file.md):

    ```cpp
    signtool  verify  /v  /kp  toaster.sys
    ```

    テスト署名、証明書が信頼された証明書と、上記の 2 つのコマンドは 1 つのエラーを生成します。

    ```cpp
    SignTool Error: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
    ```

    上記の 2 つの検証コマンドは、署名後で説明がリリースするのに便利になります。

    ドライバーは、インストールし、テスト コンピューターでテストする準備ができました。 インストール プロセス中に (Windows Vista およびそれ以降のオペレーティング システム) 用 setupapi.dev.log ファイルで詳細ログを収集するために、次のレジストリ キーが正しく設定することをお勧めは常にします。

    ```cpp
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Loglevel=0x4800FFFF
    ```

    %Systemroot% 内\\inf ファイルで、ドライバーをインストールする前に、setupapi.dev.log ファイルの名前を変更します。 インストールした後は、インストール中に貴重な情報が含まれている新しいログ setupapi.dev.log ファイルを作成するされます。

    ドライバーが正常にインストールされると、ドライバーのテスト実行できる開発用コンピューターで、またはテスト コンピューターでします。

## <a name="installing-uninstalling-and-loading-the-test-signed-driver-package"></a>インストール、アンインストール、およびテスト署名されたドライバー パッケージの読み込み


手順 2. で、システムが再起動後、テスト署名されたドライバー パッケージはインストールされ、読み込まれます。 ドライバー パッケージをインストールする 4 つの方法はあります。

1.  Dpinst (dpinst.exe) ツールは、WDK コマンド ライン ツールでドライバーをインストールするためには、再頒布可能パッケージを使用します。
2.  WDK コマンド ライン ツールでドライバーをインストールするためには、Devcon (devcon.exe) ツールを使用していない再頒布可能パッケージが。 WDK では、Devcon ツールのサンプル コードを示します。 再配布するサンプル コードから、独自の Devcon ツールを実装することができ、ツールのバージョンを再配布できます。
3.  使用して、OS には、(pnputil.exe) Pnputil ツールが用意されています。
4.  Windows の ハードウェアの追加ウィザードを使用します。

Dpinst と Pnputil 前は、Devcon と Windows のハードウェアの追加ウィザードでは、デバイスと同様に、ドライバーをインストールできますが、ドライバー パッケージをインストールします。 ドライバーをインストールする前は、OS、デバイスがコンピューターに接続されているときに、ドライバーを見つけることができます。

**DPInst を使用してドライバー パッケージをインストール (およびアンインストール) する**

1.  管理者特権のコマンド ウィンドウを開き、既定のディレクトリを c: 設定\\トースターします。
2.  Dpinst.exe は、WDK 再頒布可能パッケージのディレクトリ、x86 バージョン、amd64 バージョン、および ia64 バージョンで提供されます。 該当するバージョンを c: ドライブにコピー\\トースター ディレクトリと、次のコマンドを実行します。

    ```cpp
    dpinst.exe  /PATH  c:\toaster
    ```

    上記のコマンドでは、inf ファイルをすべてに対応するすべてのドライバーをインストールします。 使用することもできます"." 現在のディレクトリから引用符を除く。 "dpinst.exe/でしょうか"。 このツールのすべてのスイッチを示します。

    ドライバーの inf ファイルに/U スイッチは DriverStore の FileRepository からドライバー パッケージを削除 (%systemroot%\\System32\\ DriverStore\\FileRepository) ディレクトリに関連付けられているデバイスの提供、ドライバーが削除されました。 Dpinst のツール、ドライバーはドライバーの inf ファイルを参照するだけで削除できます。

    ```cpp
    dpinst.exe  /U  toaster.inf
    ```

**DevCon を使用して、ドライバー パッケージをインストールするには**

1.  管理者特権のコマンド ウィンドウを開き、既定のディレクトリを c: 設定\\トースターします。
2.  Devcon.exe は WDK バージョンのツール ディレクトリ、x86、amd64 バージョンおよび ia64 バージョンで提供されます。 該当するバージョンを c: ドライブにコピー\\トースター ディレクトリと、次のコマンドを実行します。 このコマンドは、ドライバーとデバイスにインストールされます。

    ```cpp
    devcon.exe  install <inf> <hwid>
    ```

    引用符で囲むを使用することをお勧め&lt;hwid&gt;します。 サンプルは、トースターがあります。

    ```cpp
    devcon.exe  install  c:\toaster\toaster.inf  “{b85b7c50-6a01-11d2-b841-00c04fad5171}\MsToaster”
    ```

    "Remove"スイッチを使用して Devcon ツールを使用して、デバイスを削除できます。 “devcon.exe /?” このツールのすべてのスイッチを示します。 特定の情報を取得するスイッチを使用してで「ヘルプ」は、"remove"スイッチには、次のように追加する必要があります。

    ```cpp
    devcon.exe help remove
    ```

    上記のコマンドは、次の情報を提供します。

    指定されたハードウェアまたはインスタンスの ID を持つデバイスを削除します ローカル コンピューターでのみ有効です。 (-R を含めるために必要な場合の再起動、)。

    ```cpp
    devcon [-r] remove <id> [<id>...]
    devcon [-r] remove =<class> [<id>...]
    <class>      Specifies a device setup class.
    Examples of <id>:
     *              - All devices
     ISAPNP\PNP0501 - Hardware ID
     *PNP*          - Hardware ID with wildcards  (* matches anything)
     @ISAPNP\*\*    - Instance ID with wildcards  (@ prefixes instance ID)
     '*PNP0501      - Hardware ID with apostrophe (' prefixes literal match - matches exactly as typed, including the asterisk.)
    ```

    デバイスが削除された後、ドライバーを削除する 2 つのコマンドが必要です。 "Dp_enum"スイッチを使用して最初のコマンドを使用して、ドライバー、コンピューターにインストールされたドライバー パッケージに対応する inf ファイル名を検索します。

    ```cpp
    devcon  dp_enum
    ```

    このコマンドは、oemNnn.inf ファイルをすべてに対応するドライバー パッケージ、Nnn は 10 進数字です、クラスの情報と情報を提供する、次に示すようの一覧に表示されます。

    ```cpp
    oem39.inf
        Provider: Intel
        Class: Network adapters
    oem4.inf
        Provider: Dell
        Class: ControlVault Device
    ```

    DriverStore から対応するドライバー パッケージを削除するには、以下に示した Intel「のネットワーク アダプター」について、次のコマンドを使用してドライバー。

    ```cpp
    devcon.exe dp_delete oem39.inf
    ```

**Pnputil ツールを使用して、ドライバー パッケージをインストールするには**

1.  管理者特権のコマンド ウィンドウを開き、既定のディレクトリを c: 設定\\トースターします。
2.  使用可能なすべてのスイッチを表示する次のコマンドを実行します。 スイッチの使用は、一目瞭然です例を表示する必要はありません。
    ```cpp
    C:\Windows\System32\pnputil.exe /?

    Microsoft PnP Utility
    Usage:
    ------
    pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
    Examples:
    pnputil.exe -a a:\usbcam\USBCAM.INF      -> Add package specified by USBCAM.INF
    pnputil.exe -a c:\drivers\*.inf          -> Add all packages in c:\drivers\
    pnputil.exe -i -a a:\usbcam\USBCAM.INF   -> Add and install driver package
    pnputil.exe -e                           -> Enumerate all 3rd party packages
    pnputil.exe -d oem0.inf                  -> Delete package oem0.inf
    pnputil.exe -f -d oem0.inf               -> Force delete package oem0.inf
    pnputil.exe -?                           -> This usage screen
    ```

**ハードウェアの追加ウィザードを使用して、ドライバー パッケージをインストールするには**

1.  管理者特権でコマンド ウィンドウを開きます
2.  ハードウェアの追加ウィザードを起動し、2 番目のページに移動の横にあるをクリックする hdwwiz.cpl を実行します。
3.  高度なオプションを選択し、[次へ] をクリックします。
4.  選択は、リスト ボックスからすべてのデバイスを表示し、[次へ] をクリックします
5.  ディスク オプションを選択します。
6.  パスを含む、c: フォルダーを入力します\\トースター ドライバー パッケージ
7.  Inf ファイルを選択し、[開く] をクリックしてください
8.  [OK] をクリックします。
9.  次の 2 つのページで [次へ]、インストールを完了するには、[完了] をクリックし、

**テスト署名されたドライバーが正しく動作していることを確認します。**

Toastpkg が正しく動作していることを確認します。

1.  デバイス マネージャーを起動します。
2.  トースターは、デバイスの一覧から選択します。 例については、以下のスクリーン ショットを参照してください。

    ![デバイス マネージャにトースター デバイスを示すスクリーン ショット](images/tutorialtoasterpackageindevicemgr.png)

3.  ドライバーのプロパティ ダイアログ ボックスを開くには、するには、トースター パッケージ サンプルのトースターをダブルクリックします。
4.  [全般] タブで、トースターが適切に動作していることを確認するには、状態チェック ボックスをオンします。

プロパティ ダイアログ ボックスから、デバイスとドライバーをアンインストールするのには、デバイス マネージャーを使用できます。

**テスト署名されたドライバーをトラブルシューティングする方法**

参照してください[ドライバー署名のインストールのトラブルシューティング](troubleshooting-driver-signing-installation.md)これらの手順で問題が発生した場合。









