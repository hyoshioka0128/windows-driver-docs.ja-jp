---
ms.assetid: E61BCCF7-4FC3-4F1F-9DDE-8D09F25F3EA1
title: 一般リリース用のドライバーへの署名
description: ドライバー パッケージを一般にリリースする前に、パッケージの認定依頼を提出することをお勧めします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84fa5796983bdc5aac50af88d47262906983a605
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63378620"
---
# <a name="signing-a-driver-for-public-release"></a>一般リリース用のドライバーへの署名

ドライバー パッケージを一般にリリースする前に、パッケージの認定依頼を提出することをお勧めします。 詳しくは、「[Windows ハードウェア認定キット ユーザー ガイド](https://go.microsoft.com/fwlink/p/?LinkID=248337)」および「[従来のダッシュボード](https://go.microsoft.com/fwlink/p/?LinkID=248336)」をご覧ください。 ドライバー パッケージの認定依頼を提出するには、信頼できる証明機関 (VeriSign など) から取得した証明書を使ってパッケージに署名する必要があります。 詳しくは、[VeriSign 証明書の取得に関するページ](https://go.microsoft.com/fwlink/p/?LinkID=248298)をご覧ください。 Microsoft から提供されるクロス証明書も必要です。

Verisign から、秘密キー ファイル (PVK) とソフトウェア発行元証明書 (SPC) の一対のファイルを取得済みだとします。 また、MyDriver という名前のドライバー プロジェクトと MyDriver Package という名前のドライバー パッケージ プロジェクトを含む Microsoft Visual Studio ソリューションもあるとします。 ドライバー パッケージに署名するには、次の手順を実行します。

1.  [  **Pvk2Pfx**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff550672) ツールを使って、Personal Information Exchange (PFX) 証明書を作ります。 **Pvk2Pfx** ツールは PVK ファイルと SPC ファイルを入力として取り、1 つの PFX ファイルを作ります。 この作業では、PFX ファイルの名前を MyCert.pfx とします。

    **注**  PFX ファイルを作っておくと、他のドライバー プロジェクトや他のドライバー開発コンピューターで再利用することができます。
2.  必要なクロス証明書を確認するには、[カーネル モードのコード署名用のクロス証明書に関するページ](https://go.microsoft.com/fwlink/p/?LinkID=248296)をご覧ください。 必要なクロス証明書が $(BASEDIR)\\CrossCertificates にあることを確認します。$(BASEDIR) は、Windows キットの基本ディレクトリです (c:\\Program Files (x86)\\Windows Kits\\8.0\\CrossCertificates など)。 必要なクロス証明書がない場合は、Microsoft からクロス証明書をダウンロードして $(BASEDIR)\\CrossCertificates にコピーします。
3.  Visual Studio で、MyDriver プロジェクトと MyDriver Package プロジェクトを含むソリューションを開きます。 [ソリューション エクスプローラー] ウィンドウが表示されていない場合は、 **[表示]** メニューの **[ソリューション エクスプローラー]** をクリックします。 [ソリューション エクスプローラー] ウィンドウで、パッケージ プロジェクト **[MyDriver Package]** を右クリックし、 **[プロパティ]** をクリックします。

4.  パッケージのプロパティ ページで、 **[Configuration Properties (構成プロパティ)] &gt; [Driver Signing (ドライバーの署名)] &gt; [全般]** の順に移動します。 **[Sign Mode (署名モード)]** ドロップダウン リストで、 **[Production Sign (実稼働署名)]** をクリックします。 **[Production Certificate] (実稼働証明書)** で、次のいずれかを実行します。

    -   署名証明書のパス (c:\\Certs\\MyCert.pfx など) を入力します。
    -   **[ファイルから選択]** を選び、署名証明書を参照します。
    -   **[ストアから選択]** を選び、前に証明書ストアにインポートした証明書を選択します。

        **注**  証明書をストアにインポートするには、証明書ファイル (PFX ファイル) を右クリックして、 **[PFX のインストール]** を選びます。 証明書のインポート ウィザードの指示に従います。

        **注**  後で別の証明書を使う場合は、新しい証明書が証明書ストアにインポートされていることを確認してください。 **[Select From File] (ファイルから選択)** を選択して新しい証明書を参照した場合は、新しい証明書は自動的に証明書ストアにインポートされます。 ただし、新しい証明書のパスを手動で入力した場合は、証明書ストアに自動的にはインポートされません。 この場合は、新しい証明書ファイルを右クリックして、 **[PFX のインストール]** を選ぶ必要があります。
5.  **[Driver Signing (ドライバーの署名)] &gt; [全般]**  プロパティ ページの **[TimeStampServer (TimeStampServer)]** で、ドロップダウン リストのタイムスタンプ サーバーから 1 つを選択します。

    **注**  ドロップダウン リストのタイムスタンプ サーバーのいずれかを使うには、ドライバー パッケージをビルドするときにインターネットに接続している必要があります。 ドライバー パッケージのビルド時にインターネットから切断する必要がある場合は、 **[TimeStampServer] (TimeStampServer)** フィールドをクリアします。
6.  パッケージのプロパティ ページで、 **[Configuration Properties (構成プロパティ)] &gt; [Inf2Cat] &gt; [全般]** の順に移動します。 **[Run Inf2Cat (Inf2Cat の実行)]** ドロップダウン リストで、 **[はい]** を選びます。

7.  パッケージのプロパティ ページを閉じます。
8.  ドライバー プロジェクト **[MyDriver]** を右クリックし、 **[プロパティ]** をクリックします。
9.  ドライバーのプロパティ ページで、 **[Configuration Properties (構成プロパティ)] &gt; [Driver Signing (ドライバーの署名)] &gt; [全般]** の順に移動します。 **[TimeStampServer (TimeStampServer)]** を、ドライバー パッケージのプロパティで使った値と同じ値に設定します。 **[Sign Mode] (署名モード)** を **[Production Sign] (実稼働署名)** に設定し、 **[Production Certificate] (実稼働証明書)** をドライバー パッケージのプロパティで使った値と同じ値に設定します。

10. ドライバー パッケージをビルドする準備ができたら、**F5** キーを押します。 Visual Studio によって、パッケージとドライバー ファイルが自動的に署名されます。 展開するように構成してある場合は、署名されたドライバー パッケージは Visual Studio によってテスト コンピューターに展開されます。 詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」をご覧ください。

## <a name="span-idviewingthedriverpackagefilesspanspan-idviewingthedriverpackagefilesspanspan-idviewingthedriverpackagefilesspanviewing-the-driver-package-files"></a><span id="Viewing_the_driver_package_files"></span><span id="viewing_the_driver_package_files"></span><span id="VIEWING_THE_DRIVER_PACKAGE_FILES"></span>ドライバー パッケージ ファイルの表示


ソリューションをビルドした後、エクスプローラーで、ドライバー パッケージを含むフォルダーに移動します。 パッケージ内のファイルの 1 つはカタログ ファイルです。 カタログ ファイルには、パッケージのデジタル署名が含まれています。 署名されたパッケージ内のファイルを表示する例については、「[テンプレートを使った KMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)」をご覧ください。

## <a name="span-idgettingawhqlreleasesignaturespanspan-idgettingawhqlreleasesignaturespanspan-idgettingawhqlreleasesignaturespangetting-a-whql-release-signature"></a><span id="Getting_a_WHQL_release_signature"></span><span id="getting_a_whql_release_signature"></span><span id="GETTING_A_WHQL_RELEASE_SIGNATURE"></span>WHQL リリース署名の取得


ドライバー パッケージが認定テストに合格すると、Windows Hardware Quality Labs (WHQL) がこのドライバー パッケージに署名できるようになります。 ドライバー パッケージが WHQL によって署名されると、Windows Update プログラムや Microsoft がサポートする他の配布メカニズムによって配布することができます。

Windows 10、8.1、8、7 にインストールする場合、ドライバー パッケージは SHA1 署名を 1 つ持つことができます。

Windows 10 以降では、新しい Windows 10 カーネル モード ドライバーを [Windows ハードウェア デベロッパー センター ダッシュボード ポータル](https://msdn.microsoft.com/windows/hardware/gg236587.aspx)でデジタル署名を受けるために提出する必要もあります。  カーネル モードとユーザー モードどちらのドライバーの提出でも、有効な[拡張検証 (“EV”) コード署名証明書](https://msdn.microsoft.com/library/windows/hardware/hh801887.aspx)が必要です。

**注**  SHA1 の廃止はドライバーに適用されません。  Windows での SHA1 のサポート終了について詳しくは、「[Windows における Authenticode コード署名の強制とタイムスタンプ](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-authenticode-code-signing-and-timestamping.aspx)」をご覧ください。

## <a name="span-idsigningapackagecomparedtosigninganindividualdriverfilespanspan-idsigningapackagecomparedtosigninganindividualdriverfilespanspan-idsigningapackagecomparedtosigninganindividualdriverfilespansigning-a-package-compared-to-signing-an-individual-driver-file"></a><span id="Signing_a_package_compared_to_signing_an_individual_driver_file"></span><span id="signing_a_package_compared_to_signing_an_individual_driver_file"></span><span id="SIGNING_A_PACKAGE_COMPARED_TO_SIGNING_AN_INDIVIDUAL_DRIVER_FILE"></span>パッケージへの署名と個々のドライバー ファイルへの署名の比較


ドライバー パッケージには、複数のファイルが含まれます。 ドライバー パッケージには通常、1 つ以上のドライバー ファイル、情報ファイル (INF ファイル)、カタログ ファイルが含まれます。 カタログ ファイルには、パッケージ内の他のファイルに関する情報が含まれています。 カタログ ファイルに署名すると、カタログ ファイル内の署名は、ドライバー パッケージ全体の署名として機能します。 つまり、"*カタログ ファイルへの署名*" は "*ドライバー パッケージへの署名*" と同じです。

ほとんどの場合、ドライバー パッケージに署名すれば十分で、個々のドライバー ファイルに署名する必要はありません。 ただし、パッケージと個々のドライバー ファイルの両方への署名が必要になる場合があります。 たとえば、ブート開始ドライバー ファイルは、個々のファイルに署名する必要があります。 個々のドライバー ファイルへの署名は、"*ドライバー ファイルへの署名の埋め込み*" と呼ばれます。

MyDriver という名前のドライバー プロジェクトと MyDriver Package という名前のドライバー パッケージ プロジェクトを含む Microsoft Visual Studio ソリューションがあるとします。 Visual Studio には、MyDriver 用と MyDriver Package 用の 2 つのプロパティ ページが用意されています。 ドライバー パッケージに署名するには、MyDriver Package の **[ドライバーの署名]** プロパティを設定します。 個々のドライバー ファイルに署名を埋め込むには、MyDriver の **[ドライバーの署名]** プロパティを設定します。

ドライバー パッケージのプロパティを実稼働署名に設定するときは、それに応じて個々のドライバー ファイルの署名プロパティも調整する必要があります。 個々のドライバー ファイルの署名を無効にするか、または個々のドライバー ファイルがパッケージに対して指定したものと同じ証明書を使うように設定します。

**注**  証明書のハッシュ (拇印とも呼ばれます) を確認するには、コマンド プロンプト ウィンドウを開いて、証明書を含むディレクトリに移動します。 コマンド「**certutil -dump** *CertName.pfx*」を入力します。*CertName.pfx* は証明書の名前です。

     

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Windows 10 のドライバー署名の変更点](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/04/01/driver-signing-changes-in-windows-10.aspx)
* [Windows 7 および Windows Server 2008 R2 で SHA-2 コード署名サポートを利用可能](https://technet.microsoft.com/library/security/3033929)
* [ドライバーへの署名](signing-a-driver.md)
* [Windows ハードウェア認定](https://go.microsoft.com/fwlink/p/?LinkID=248337)
* [ハードウェア ダッシュボード サービス](https://go.microsoft.com/fwlink/p/?LinkID=248336)
* [Windows のドライバー署名の要件](https://go.microsoft.com/fwlink/p/?linkid=617515)
* [カーネル モードのコード署名のクロス証明書](https://go.microsoft.com/fwlink/p/?LinkID=248296)
* [カーネル モードのコード署名の手順](https://go.microsoft.com/fwlink/p/?linkid=617516)
* [ドライバーの署名](https://msdn.microsoft.com/Library/Windows/Hardware/Ff544865)
* [ブート開始ドライバーのインストール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547570)
* [ドライバーの署名用ツール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552958)
 

 




