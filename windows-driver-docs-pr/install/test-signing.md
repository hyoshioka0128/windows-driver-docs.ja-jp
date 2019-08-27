---
title: テスト署名
description: Windows 64-bit edition では、ドライバーを含め、カーネルモードで実行されているすべてのソフトウェアが、デジタル署名されている必要があります。
ms.assetid: 52F309E4-9553-456B-BBD6-217318FC7222
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf77cdb05cc6ff7c2354835d56a7f8d6cf2eb41e
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025348"
---
# <a name="test-signing"></a>テスト署名


Windows Vista 以降では、x64 ベースのバージョンの Windows では、ドライバーを含め、カーネルモードで実行されているすべてのソフトウェアに対して、デジタル署名を行う必要がありました。 最初に、F8 スイッチ (各ブートでは Windows が読み込まれる前) を使用して、ドライバーに有効な署名が必要な読み込み時の強制を無効にすることができます。 しかし、最初のいくつかの使用後は面倒になります。 カーネルデバッガーをテストコンピューターにアタッチすると、正しい BCDEdit コマンドを使用した後に、同じ読み込み時の強制チェックを無効にすることができます。 ただし、最終的には、開発中にドライバーのテスト署名が必要になり、最終的にドライバーをリリースしてからユーザーに公開する必要があります。

## <a name="installing-an-unsigned-driver-during-development-and-test"></a>開発中およびテスト中の署名されていないドライバーのインストール


*抜粋*[開発およびテスト中の署名](installing-an-unsigned-driver-during-development-and-test.md)されていないドライバーのインストール:

既定では、Windows Vista 以降のバージョンの windows では64、カーネルがドライバーの署名を確認できる場合にのみ、カーネルモードドライバーが読み込まれます。 ただし、初期のドライバーの開発時や自動テスト以外の場合は、この既定の動作を無効にすることができます。 開発者は、次のいずれかのメカニズムを使用して、有効なドライバー署名の読み込み時の適用を一時的に無効にすることができます。 ただし、プラグアンドプレイ (PnP) によってインストールされたドライバーのテストを完全に自動化するには、ドライバーの[カタログファイル](catalog-files.md)が署名されている必要があります。 Windows Vista 以降のバージョンの Windows では、署名されていないドライバーに対して、システム管理者がドライバーのインストールを承認する必要があるドライバー署名ダイアログボックスが表示されるため、ドライバーの署名が必要になります。ドライバーのインストールとデバイスの使用に必要な特権。 Windows Vista 以降のバージョンの Windows では、この PnP ドライバーのインストール動作を無効にすることはできません。

### <a name="use-the-f8-advanced-boot-option"></a>**F8 の詳細ブートオプションを使用する**

Windows Vista 以降のバージョンの Windows では、[ドライバー署名の強制を無効にする] という F8 の詳細ブートオプションがサポートされています。これにより、現在のシステムセッションに対してのみカーネルモードドライバーの読み込み時署名の適用が無効になります。 この設定は、システムを再起動しても保持されません。

再起動時に、ドライバー署名の強制を無効にするオプションを指定して、次のブートオプション画面が表示されます。 このプロビジョニングによって、テスト目的で署名されていないドライバーをインストールできるようになります。

![f8 の詳細ブートオプションを示すスクリーンショット](images/tutorialf8.png)

### <a href="" id="attach-a-kernel-debugger-to-disable-signature-verification"></a>カーネルデバッガーをアタッチして署名の検証を無効にする

アクティブなカーネルデバッガーを開発またはテスト用コンピューターにアタッチすると、カーネルモードドライバーの読み込み時の署名の適用が無効になります。 このデバッグ構成を使用するには、次のコマンドを実行して、開発用コンピューターまたはテスト用コンピューターにデバッグコンピューターをアタッチし、開発またはテスト用コンピューターでカーネルデバッグを有効にします。

```cpp
bcdedit -debug on
```

BCDEdit を使用するには、ユーザーがシステムの Administrators グループのメンバーであり、管理者特権でのコマンドプロンプトからコマンドを実行する必要があります。 管理者特権でのコマンドプロンプトウィンドウを開くには、 *cmd.exe*へのデスクトップショートカットを作成し、ショートカットを右クリックして、 **[管理者として実行]** を選択します。

ただし、開発者がカーネルデバッガーをアタッチする必要がある場合もありますが、ロード時の署名の強制を維持する必要もあります。 「 [付録 1:カーネルモード署名の検証をカーネルデバッグモード](appendix-1--enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode.md)で実行し、これを実現する方法について説明します。

## <a name="test-sign-a-driver-package"></a>ドライバーパッケージのテスト署名


上記の2つの方法を使用してドライバー署名の強制要件を回避するのではなく、ドライバーパッケージの署名をテストすることをお勧めします。 テスト署名とドライバーのインストールは開発用コンピューターで実行できますが、2台のコンピューター (1 つは開発と署名用、もう1つはテスト用) が必要になる場合があります。

*抜粋*[ドライバパッケージのテスト署名方法](how-to-test-sign-a-driver-package.md):

<a href="" id="signing-computer"></a>**署名コンピューター**  
これは、Windows Vista 以降のバージョンの Windows でドライバーパッケージをテストするために使用されるコンピューターです。 このコンピューターでは、Windows XP SP2 以降のバージョンの Windows が実行されている必要があります。 [ドライバー署名ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-signing-drivers)を使用するには、このコンピューターに windows Vista 以降のバージョンの Windows driver KIT (WDK) がインストールされている必要があります。 開発用コンピューターにすることもできます。

<a href="" id="test-computer"></a>**テストコンピューター**  
これは、テスト署名されたドライバーパッケージをインストールしてテストするために使用されるコンピューターです。 このコンピューターでは、Windows Vista 以降のバージョンの Windows が実行されている必要があります。

## <a name="test-signing-procedure"></a>テスト署名の手順


ドライバーパッケージには、ドライバーバイナリ、INF ファイル、CAT ファイル、およびその他の必要なファイルが含まれます。 ドライバーパッケージには、ドライバーが複数のターゲットプロセッサの種類用に構築されている場合は、x86、AMD64、IA64 などのサブディレクトリが含まれる場合があります。 開発/署名コンピューターを使用して、次の手順を実行します。

次の手順では、ドライバーパッケージへの署名をテストする手順について説明します。

1.  ターゲットのドライバーをビルドします。 Windows 8.0 または Windows 8.1 用のドライバーをビルドする場合は、Visual Studio 2012 を使用するか、対応する WDK (Windows 8.0 または 8.1 WDK など) と共に Visual Studio 2013 してください。

    以下で説明するコマンドツールはすべて、Visual Studio 2012 または Visual Studio 2013 対応するツール/ビルドコマンドウィンドウから使用する必要があります。

    **メモ** Command tools for Visual Studio は、install directory、C: Program Files (\\x86)\\Microsoft Visual Studio 12.0\\Common7\\tools\\のショートカットにあります。




コマンドプロンプトの5つのショートカットのいずれかに、makecert、inf2cat、signtool、certmgr.exe などのコマンドがあります。

最も一般的な "開発者コマンドプロンプト for VS2013" を選択できます。 ショートカットをタスクバーにピン留めして、簡単にアクセスできるようにすることができます。

**メモ** ただし、Visual Studio では、ドライバーの署名のコマンドツールのアプローチではなく、Visual Studio 2013 開発環境 (IDE とも呼ばれます) を使用してドライバーパッケージに署名することもできます。 付録2を[参照してください。詳細については](appendix-2--signing-drivers-with-visual-studio.md) 、「Visual Studio でドライバーに署名する」を参照してください。




2.  ドライバーパッケージフォルダーを作成し、ドライバーファイルをコピーして、必要なサブディレクトリ (C:\\drivertestpackage など) を保持します。
3.  ドライバーパッケージ用の inf ファイルを作成します。 Inf ファイルの日付が、Vista の場合は08/21/2006 以前ではなく、Windows 8.0、Windows 8.1、Windows 7.0 および Windows 7.1 の場合は、その後の日付であることを確認してください。 Inf ファイルの chkinf ツールを使用して inf ファイルをテストし、エラーが報告されないようにすることをお勧めします。 プリンタードライバーの場合は、ツール chkinf を使用して inf ファイルをテストし、WDK からを実行します。
4.  *抜粋*[テスト証明書の作成](creating-test-certificates.md):

    次のコマンドラインの例では、MakeCert を使用して、次のタスクを実行します。

    -   *Contoso .com (test)* という名前の自己署名テスト証明書を作成します。 この証明書では、サブジェクト名と証明機関 (CA) に同じ名前が使用されます。

    -   *ContosoTest*という名前の出力ファイルに証明書のコピーを配置します。

    -   *PrivateCertStore*という名前の証明書ストアに証明書のコピーを配置します。 テスト証明書を*PrivateCertStore*に配置すると、システム上にある他の証明書とは分離されます。

    次の MakeCert コマンドを使用して、 *Contoso .com (テスト)* 証明書を作成します。

    ```cpp
    makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) ContosoTest.cer
    ```

    各項目の意味は次のとおりです。

    -   **-R**オプションを指定すると、同じ発行者とサブジェクト名を持つ自己署名証明書が作成されます。

    -   **-Pe**オプションは、証明書に関連付けられている秘密キーをエクスポートできることを指定します。

    -   **-Ss**オプションは、テスト証明書 (*PrivateCertStore*) を含む証明書ストアの名前を指定します。

    -   **-N CN =** オプションは、証明書の名前 (Contoso .com) を指定します。 この名前は、証明書を識別するために[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)ツールと共に使用されます。

    -   *ContosoTest*は、テスト証明書 (Contoso .com) のコピーを含むファイル名です。 証明書ファイルは、信頼されたルート証明機関の証明書ストアおよび信頼された発行元の証明書ストアに証明書を追加するために使用されます。

    *抜粋*[テスト証明書の表示](viewing-test-certificates.md):

    証明書が作成され、証明書ストアにコピーが格納されたら、Microsoft 管理コンソール (MMC) の証明書スナップインを使用して証明書を表示できます。 MMC**証明書**スナップインを使用して証明書を表示するには、次の手順を実行します。

    1.  **スタート** をクリックし、検索の開始 をクリックします。

    2.  証明書スナップインを開始するには、「Certmgr.exe」と入力し、 **enter**キーを押します。

    3.  証明書スナップインの左側のウィンドウで、[PrivateCertStore certificate store] フォルダーを展開し、[Certificates] をダブルクリックします。

    次のスクリーンショットは、 **PrivateCertStore**証明書ストアフォルダーの証明書スナップインビューを示しています。

    ![テスト証明書が表示されている証明書ストアのスクリーンショット ](images/tutorialprivatecertstore.png)

    Contoso .com (Test) 証明書の詳細を表示するには、右側のウィンドウで証明書をダブルクリックします。 次のスクリーンショットは、証明書の詳細を示しています。

    ![contoso.com (テスト) 証明書に関する全般的な情報を表示している [証明書] ウィンドウのスクリーンショット](images/tutorialcertificategeneraltab.png)

    [証明書] ダイアログボックスに次のような状態が表示されます。"この CA ルート証明書は信頼されていません。 信頼を有効にするには、この証明書を [信頼されたルート証明機関] ストアにインストールします。 これは想定される動作です。 Windows が発行機関 "Contoso .com (Test)" を既定で信頼していないため、証明書を検証できません。

5.  カタログファイル (.cat 拡張子) を作成します。 次のように inf2cat ツールを使用して、カタログファイルを作成します。 スイッチにはスペースを使用できないことに注意して&lt;ください。&gt;/driver:&gt;空白&lt;の完全パス&lt;、/os&gt;::&gt;no space&lt; &lt;os1 name、:space&gt;&gt;os2 の名前がありません。&lt;

    ```cpp
    inf2cat  /v  /driver:C:\DriverTestPackage  /os:7_64,7_x86 ,XP_X86
    ```

    これにより、ドライバーの .inf ファイルで指定された名前のカタログファイルが作成されます。 追加のコンマ区切り Os は、次に示すように、選択的に追加することも、スペースを入れずに追加することもできます。

    ```cpp
    /os:2000,XP_X86,XP_X64,Server2003_X64,Vista_X64,Vista_X86,7_x86,7_64,Server2008_x86,Server2008_x64,Sever2008_IA64,Server2008R2_x86,Server2008R2_x64,Server2008R2_IA64,8_x86,8_x64, 8_ARM, Server8_x64
    ```

    新しい 8.1 WDK から更新された inf2cat には、/os のオプション値として、663X86、63X64、633ARM、および SERVER_6_3_X64 があります。

    Version セクションの INF ファイルの例。

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

    /Driver (または/drv) オプションは、1つまたは複数の INF ファイルを含むディレクトリを指定します。 このディレクトリ内で、1つまたは複数の CatalogFile ディレクティブが含まれている INF ファイルに対して、カタログファイルが作成されます。 カタログファイル名は、8.3 の名前に制限されていません。

    コマンドライン引数/os: 7Inf2Cat が使用されている場合、カタログファイル tstamd64.cat が作成されます。 同様に、Server2008R2_IA64 の場合と同様に、/os: XP_X86, オプションが使用されている場合、このツールはカタログファイル toastx86.cat を作成します。 1つのカタログファイルのみが必要な場合は、次に示すように、INF ファイル内のエントリは1つだけで十分です。

    ```cpp
    CatalogFile.NT  = toaster.cat
    ```

    または

    ```cpp
    CatalogFile = toaster.cat
    ```

    INF ファイル内の日付が OS リリース日よりも大きい場合、inf2cat ツールによって、Windows 7 用の/os パラメーターが以前の日付である場合に、次のエラーが報告されます。

    ```cpp
    Signability test failed.
    Errors:
    22.9.7: DriverVer set to incorrect date (must be postdated to 4/21/2009 for newest OS) in \toaster.inf
    ```

    Inf2cat ツールは、各フォルダーとサブフォルダーで、INF ファイルにエントリがあるすべてのファイルの存在を確認する場合に非常に厳格です。 このような不足しているエントリには、意味のあるエラーメッセージが表示されます。

    Cat ファイルは、エクスプローラーから開くことができます。そのためには、ダブルクリックするか、ファイルを右クリックして [開く] を選択します。 [セキュリティ] タブには、GUID 値を含むいくつかのエントリが表示されます。 GUID 値を選択すると、次に示すように、ドライバーパッケージのドライバーファイルと追加された Os を含む詳細が表示されます。

    ```cpp
    OSAttr  2:5.1,6.1
    ```

    番号5.1 は XP OS のバージョン番号、Windows 7.0 OS の場合は6.1 です。

    Cat ファイルをチェックして、ドライバーファイルと選択した Os が含まれていることを確認することをお勧めします。 ドライバーファイルを追加または削除した場合はいつでも、INF ファイルが変更されているため、cat ファイルを再作成して再度署名する必要があります。 ここで省略した場合、インストールエラーが発生します。これは、セットアップログファイル (Vista 以降の場合は setupapi.log、XP の場合は setupapi.log ファイル) で報告されます。

6.  *抜粋*[ドライバーパッケージのカタログファイルのテスト署名](test-signing-a-driver-package-s-catalog-file.md):

    次のコマンドラインは、SignTool を実行して次の操作を実行する方法を示しています。

    -   *Toastpkg*サンプル[ドライバーパッケージ](driver-packages.md)の*tstamd64.cat*カタログファイルにテスト署名します。 この[カタログファイル](catalog-files.md)の作成方法の詳細については、「[ドライバーパッケージのテスト署名用のカタログファイルの作成](creating-a-catalog-file-for-test-signing-a-driver-package.md)」を参照してください。

    -   テスト署名には、PrivateCertStore の Contoso .com (Test) 証明書を使用します。 この証明書の作成方法の詳細については、「[テスト証明書の作成](creating-test-certificates.md)」を参照してください。

    -   タイムスタンプ機関 (TSA) を使用したデジタル署名のタイムスタンプ。

    *Tstamd64.cat*カタログファイルのテストに署名するには、次のコマンドラインを実行します。

    ```cpp
    Signtool sign /v /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com tstamd64.cat
    ```

    各項目の意味は次のとおりです。

    -   **Sign**コマンドは、指定されたカタログファイル tstamd64.cat に署名するように SignTool を構成します。

    -   **/V**オプションは、SignTool が成功した実行と警告メッセージを表示する詳細な操作を有効にします。

    -   **/S**オプションは、テスト証明書を含む証明書ストア (*PrivateCertStore)* の名前を指定します。

    -   **/N**オプションは、指定された証明書ストアにインストールされている証明書 (*Contoso .com (Test))* の名前を指定します。

    -   **/T**オプションは、デジタル署名のタイムスタンプ *http://timestamp.digicert.com* となる TSA () の URL を指定します。
        **重要**  タイムスタンプを含めると、署名者のコード署名の秘密キーが侵害された場合にキーを失効させるために必要な情報が提供されます。




-   *tstamd64.cat*は、デジタル署名されるカタログファイルの名前を指定します。

tstamd64.cat は、デジタル署名されるカタログファイルの名前を指定します。 前の説明に従って、cat ファイルを開くことができます。


7.  *変更*された抜粋[埋め込み署名を使用したドライバーのテスト署名](test-signing-a-driver-through-an-embedded-signature.md):

    -   Windows Vista 以降のバージョンの windows 64 では、カーネルモードのコード署名の要件には、埋め込まれた署名が必要です。 これは、ドライバーのドライバーパッケージにデジタル署名されたカタログファイルがあるかどうかに関係なく必要です。

    カーネルモードドライバーのバイナリファイルに署名するコマンドを次に示します。

    ```cpp
    signtool sign  /v  /s  PrivateCertStore  /n  Contoso.com(Test)  /t http://timestamp.verisign.com/scripts/timestamp.dll   amd64\toaster.sys
    ```

    amd64\\トースターは、埋め込み署名されるカーネルモードバイナリファイルの名前を指定します。

    WDK 7.1 インストールディレクトリ内では、トースターサンプルは src\\general\\トースター\\toastpkg\\toastpkg\\ディレクトリにあります。 Windows 8 または 8.1 WDK のサンプルは、Microsoft ダウンロードサイトからダウンロードされます。 これらのサンプルには、Windows 8 または 8.1 Windows Driver Kit は付属していません。

    Windows エクスプローラーでファイルをダブルクリックしてカタログファイルを開くと、次のスクリーンショットが表示されます。 [署名の表示] が強調表示されていることに注意してください。

    ![セキュリティカタログファイルの一般的な情報を示すスクリーンショット](images/tutorialsecuritycatalogfilegeneraltab.png)

    [署名の表示] をクリックすると、以下のスクリーンショットが表示され、[証明書の表示] から次の表示オプションが提供されます。これにより、ダイアログ自体の [証明書のインストール] オプションが表示されます。 ここでは、certmgr.exe ツールを使用して証明書をインストールするための、推奨されるコマンドラインオプションを提供しています。

    ![デジタル署名の詳細に関する一般的な情報を示すスクリーンショット](images/tutorialdriversignaturedetails.png)

    ![証明書に関する一般的な情報を示すスクリーンショット](images/tutorialcertificategeneraltab.png)

これで、署名コンピューターまたはテストコンピューターでドライバーをテストできるようになりました。 テストコンピューターを使用している場合は、ファイル構造をそのまま維持した状態で、ドライバーパッケージをコンピューターにコピーします。 ツール certmgr.exe もテストコンピューターにコピーする必要があります。 テストコンピューターを使用する場合は、テスト署名された toastpkg ドライバーパッケージを c\\: トースター一時フォルダーにコピーします。

次の手順では、どちらのコンピューターでもドライバーをテストするために使用する手順について説明します。

1.  管理者特権のコマンドウィンドウで、次のコマンドを実行します。

    ```cpp
    bcdedit  /set  testsigning  on
    ```

    コンピューターを再起動します。

2.  *選択された抜粋の開始*[Certmgr.exe を使用してテストコンピューターにテスト証明書をインストールするに](using-certmgr-to-install-test-certificates-on-a-test-computer.md)は:

    ドライバーの[テスト署名](test-signing-driver-packages.md)に使用された証明書 ( *.cer*) ファイルをテストコンピューターにコピーします。 証明書ファイルは、テストコンピューター上の任意のディレクトリにコピーできます。

    次の Certmgr.exe コマンドは、証明書ファイル*Certificatefilename .cer*の証明書を、テストコンピューターの信頼されたルート証明機関の証明書ストアに追加します。

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine root
    ```

    次の Certmgr.exe コマンドは、証明書ファイル*Certificatefilename .cer*の証明書を、テストコンピューターの信頼された発行元の証明書ストアに追加します。

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
    ```

    Where ( [**certmgr.exe**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)*からの抜粋*):

    /add のある Ename

    指定した証明書ファイルの証明書を証明書ストアに追加します。

    /s

    証明書ストアがシステムストアであることを指定します。

    /r RegistryLocation

    システムストアのレジストリの場所が HKEY_LOCAL_MACHINE の下にあることを指定します。

    CertificateStore

    証明書ストアを指定します。 trustedpublisher は、"localMachine root" の場合と同様です。

    コンピューターを再起動します。 これで、Certmgr.exe を実行して、上の2つの場所に ContosoTest が表示されていることを確認できます。 証明書が表示されない場合、証明書をインストールするもう1つの方法として、証明書を開き、上記の2つのノードにインストールして、もう一度確認します。

3.  Cat ファイルと sys ファイルの署名を確認します。 管理者特権のコマンドウィンドウを開き、コンピューターで signtool が使用可能であることを前提として、cat、inf、および sys ファイルが配置されているドライバーパッケージディレクトリに移動します。 適切なディレクトリで次のコマンドを実行します。

    次のように[、カタログファイルの SPC 署名を検証し](verifying-the-spc-signature-of-a-catalog-file.md)ます。

    ```cpp
    signtool  verify  /v  /kp  /c  tstamd64.cat  toaster.inf
    ```

    埋め込み記号を確認するには、次のコマンドを実行します。

    [リリース署名されたドライバーファイルの署名の検証](verifying-the-signature-of-a-release-signed-driver-file.md)から:

    ```cpp
    signtool  verify  /v  /kp  toaster.sys
    ```

    上記の2つのコマンドでは、テストに署名され、証明書が信頼された証明書ではないため、1つのエラーが生成されます。

    ```cpp
    SignTool Error: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
    ```

    上記の2つの検証コマンドは、後で説明するリリース署名で非常に役に立ちます。

    これで、テストコンピューターにドライバーをインストールしてテストする準備ができました。 インストールプロセス中に、(Windows Vista 以降のオペレーティングシステムの) setupapi.log ファイルで詳細ログを収集するには、次のレジストリキーが適切に設定されていることを常にお勧めします。

    ```cpp
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Loglevel=0x4800FFFF
    ```

    % SystemRoot%\\inf ファイルで、ドライバーをインストールする前に、setupapi.log ファイルの名前を変更します。 インストールが完了すると、インストール中に発生した重要な情報を含む新しいログファイルが作成されます。

    ドライバーが正常にインストールされると、開発用コンピューターまたはテストコンピューターで、ドライバーのテストを実行できるようになります。

## <a name="installing-uninstalling-and-loading-the-test-signed-driver-package"></a>テスト署名されたドライバーパッケージのインストール、アンインストール、および読み込み


手順 2. でシステムを再起動した後、テスト署名されたドライバーパッケージをインストールして読み込むことができます。 ドライバーパッケージをインストールするには、次の4つの方法があります。

1.  Dpinst (Dpinst) ツールを使用します。これは、ドライバーをインストールするための WDK コマンドラインツールであり、再頒布可能です。
2.  Devcon (devcon) ツールを使用します。これは、ドライバーをインストールするための WDK コマンドラインツールですが、再頒布可能ではありません。 Devcon ツールのサンプルコードは、WDK で提供されています。 再配布するには、サンプルコードから独自の Devcon ツールを実装し、ツールのバージョンを再配布することができます。
3.  OS 提供の Pnputil (pnputil) ツールを使用します。
4.  Windows ハードウェアの追加ウィザードを使用する。

Dpinst と Pnputil によってドライバーパッケージがインストールされます。一方、Devcon および Windows ハードウェアの追加ウィザードでは、ドライバーとデバイスをインストールすることができます。 ドライバーを事前にインストールすると、デバイスがコンピューターに接続されている場合、OS はドライバーを見つけることができます。

**DPInst を使用してドライバーパッケージをインストール (およびアンインストール) するには**

1.  管理者特権のコマンドウィンドウを開き、既定のディレクトリを\\c: トースターに設定します。
2.  Dpinst は、WDK バージョン、amd64 バージョン、および ia64 バージョンの WDK redist ディレクトリに用意されています。 関連するバージョンを c:\\トースターディレクトリにコピーし、次のコマンドを実行します。

    ```cpp
    dpinst.exe  /PATH  c:\toaster
    ```

    上記のコマンドは、すべての inf ファイルに対応するすべてのドライバーをインストールします。 "." を使用することもできます。 現在のディレクトリからの引用符がありません。 "dpinst/?" このツールのすべてのスイッチを表示します。

    ドライバーの inf ファイルにある/u スイッチを使用すると、ドライバーパッケージが driverstore の FileRepository (% SystemRoot\\%\\ System32 driverstore\\FileRepository) ディレクトリから削除されます。ドライバーが削除されました。 Dpinst ツールを使用すると、ドライバーの inf ファイルを参照するだけでドライバーを削除できます。

    ```cpp
    dpinst.exe  /U  toaster.inf
    ```

**DevCon を使用してドライバーパッケージをインストールするには**

1.  管理者特権のコマンドウィンドウを開き、既定のディレクトリを\\c: トースターに設定します。
2.  Devcon は、WDK ツールディレクトリの x86 バージョン、amd64 バージョン、および ia64 バージョンで提供されています。 関連するバージョンを c:\\トースターディレクトリにコピーし、次のコマンドを実行します。 このコマンドでは、デバイスだけでなくドライバーもインストールされます。

    ```cpp
    devcon.exe  install <inf> <hwid>
    ```

    &lt;Hwid&gt;の周りに引用符を使用することをお勧めします。 トースターサンプルの場合、次のようになります。

    ```cpp
    devcon.exe  install  c:\toaster\toaster.inf  “{b85b7c50-6a01-11d2-b841-00c04fad5171}\MsToaster”
    ```

    デバイスは、"削除" スイッチを使用して、Devcon ツールを使用して削除できます。 "devcon/?" このツールのすべてのスイッチを表示します。 特定の情報を取得するには、"削除" スイッチのスイッチ "help" を使用して、次のように追加する必要があります。

    ```cpp
    devcon.exe help remove
    ```

    上記のコマンドは、次の情報を提供します。

    指定されたハードウェアまたはインスタンス ID を持つデバイスを削除します。 ローカルコンピューター上でのみ有効です。 (必要に応じて再起動するには、-r を含めます)。

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

    デバイスが削除された後、ドライバーを削除するには、2つのコマンドが必要です。 "Dp_enum" スイッチを指定した最初のコマンドを使用して、コンピューターにインストールされているドライバーパッケージに対応するドライバーの inf ファイル名を検索します。

    ```cpp
    devcon  dp_enum
    ```

    このコマンドは、ドライバーパッケージに対応するすべての oemNnn .inf ファイルの一覧を表示します。 Nnn は、次に示すように、クラス情報と提供情報を含む10進数です。

    ```cpp
    oem39.inf
        Provider: Intel
        Class: Network adapters
    oem4.inf
        Provider: Dell
        Class: ControlVault Device
    ```

    対応するドライバーパッケージを DriverStore から削除するには、次に示す Intel "Network Adapters" ドライバーの次のコマンドを使用します。

    ```cpp
    devcon.exe dp_delete oem39.inf
    ```

**PnpUtil を使用してドライバーパッケージをインストールするには**

1.  管理者特権のコマンドウィンドウを開き、既定のディレクトリを\\c: トースターに設定します。
2.  次のコマンドを実行すると、使用可能なすべてのスイッチが表示されます。 スイッチの使用方法はわかりやすく、例を示す必要はありません。
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

**ハードウェアの追加ウィザードを使用してドライバーパッケージをインストールするには**

1.  管理者特権のコマンドウィンドウを開く
2.  Hdwwiz を実行して、ハードウェアの追加ウィザードを起動し、[次へ] をクリックして2番目のページにアクセスします。
3.  詳細オプションを選択し、[次へ] をクリックします。
4.  リストボックスから [すべてのデバイスを表示] を選択し、[次へ] をクリックします。
5.  [ディスクを含める] オプションを選択します。
6.  C: トースター driver パッケージが格納されている\\フォルダーへのパスを入力します。
7.  Inf ファイルを選択し、[開く] をクリックします。
8.  [OK] をクリックします。
9.  次の2つのページで [次へ] をクリックし、[完了] をクリックしてインストールを完了します。

**テスト署名されたドライバーが正しく動作していることを確認する**

Toastpkg が正しく動作していることを確認するには、次のようにします。

1.  デバイスマネージャーの開始
2.  デバイスの一覧から [トースター] を選択します。 例については、次のスクリーンショットを参照してください。

    ![デバイスマネージャーのトースターデバイスを示すスクリーンショット](images/tutorialtoasterpackageindevicemgr.png)

3.  ドライバーの [プロパティ] ダイアログボックスを開くには、トースター Package Sample トースターをダブルクリックします。
4.  トースターが正しく機能していることを確認するには、[全般] タブで、[状態] ボックスをオンにします。

デバイスマネージャーを使用して、[プロパティ] ダイアログボックスからデバイスとドライバーをアンインストールできます。

**テスト署名されたドライバーのトラブルシューティング方法**

これらの手順で問題が発生した場合は、「[ドライバー署名のインストールのトラブルシューティング](troubleshooting-driver-signing-installation.md)」を参照してください。









