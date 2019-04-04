---
title: リリース署名
description: 署名とドライバーのリリースできる可能性の確認、テストの完了、ドライバー パッケージが署名されたリリースします。 ドライバー パッケージに署名するリリースの 2 つの方法はあります。
ms.assetid: 71499A0A-95D0-411C-84D1-C4B91FA4E6B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccf11cd9c23287cef6b1bdd7a7e130420d21665f
ms.sourcegitcommit: c7fd0b78f613ffa76ae9f2c00fdc9fa77574269b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665795"
---
# <a name="release-signing"></a>リリース署名


署名とドライバーのリリースできる可能性の確認、テストの完了、ドライバー パッケージが署名されたリリースします。 ドライバー パッケージに署名するリリースの 2 つの方法はあります。

Windows Vista に読み込まれるカーネル モードまたはユーザー モードのバイナリ (たとえば、.sys または .dll ファイル) のパブリッシャーと以降のバージョンの Windows リリース署名を識別します。

カーネル モード バイナリは、いずれかでリリース署名です。

1.  Windows ハードウェア品質 Lab (WHQL Winqual とも呼ばれます) を解放するドライバー パッケージに署名します。 WHQL リリース署名は、Windows 認定プログラムを通じて取得されます。 次のリンクでは、最初から Windows 認定プログラムの最後の 5 つの手順について説明します。 参照してください[Windows ハードウェア認定: ここから始めて](https://msdn.microsoft.com/windows/hardware/hh833792)このオプションの詳細についてはします。 上記のリンクの手順の質問に回答に送られる<sysdev@microsft.com>エイリアス。
2.  WHQL プログラムを使用する代わりに、ドライバー パッケージはドライバー開発者やベンダーによって署名されたリリースを指定できます。 このプログラムは、Vista OS のリリースから開始しました。 ソフトウェア発行元証明書 (SPC) を介してリリース署名が作成されます。 SPC は、マイクロソフトがこのような証明書を発行する権限を持つサード パーティ証明機関 (CA) から取得されます。 SPC のこの種類で生成された署名は、64 ビットおよび 32 ビットのバージョンの Windows Vista と Windows の以降のバージョンの PnP ドライバー署名要件にも準拠します。

サインインの方法 2 のドライバー パッケージのリリースに必要な手順について説明します。

## <a name="obtain-a-software-publisher-certificate-spc"></a>ソフトウェア発行元証明書 (SPC) の取得します。


リリースの署名とも呼ばれるソフトウェア発行元証明書 (SPC) として、商用 CA からコード署名証明が必要です。

[カーネル モード コード署名用クロス証明書](cross-certificates-for-kernel-mode-code-signing.md)トピックでは、Microsoft によって承認されているサード パーティ証明機関 (CA) の一覧を提供します。 記号のドライバー パッケージをリリースするソフトウェア発行元証明書 (SPC) を提供する CA ベンダーを一覧表示を使用する必要があります。

SPC を取得し、署名のコンピューターに、秘密キーをインストールする方法について、CA の手順に従います。 SPC が、ドライバー パッケージに署名するために要求したドライバーのベンダーの独自のインストルメント化であるに注意してください。 SPC、秘密キー、およびパスワードを要求元の仕入先の組織外のユーザーと共有できません必要があります。

## <a name="cross-certificates"></a>クロス証明書


*抜粋*[ソフトウェア発行元証明書](software-publisher-certificate.md):

SPC を入手すると、だけでなく、クロス証明書は Microsoft によって発行されるを取得する必要があります。 クロス証明書は、SPC を発行した CA が信頼されたルート機関であることを確認に使用されます。 クロス証明書は、別の CA のルート証明書の公開キーを署名する CA によって発行された X.509 証明書です。 クロス証明書は、単一信頼された Microsoft ルート機関、SPCs を発行する商用の Ca を信頼チェーンを拡張する柔軟性も備えていて、システムを許可します。

発行元をクロス証明書を配布する必要はありません、[ドライバー パッケージ](driver-packages.md)します。 クロス証明書は、ドライバー パッケージのデジタル署名に含まれている[カタログ ファイル](catalog-files.md)またはドライバーのファイルに埋め込まれている署名します。 ドライバー パッケージをインストールするユーザーは、クロス証明書の使用による追加の構成手順を実行する必要はありません。

*抜粋を選択した*[カーネル モード コード署名用クロス証明書](cross-certificates-for-kernel-mode-code-signing.md):

クロス証明書は、1 つ証明書機関 (CA) によって別の証明書機関のルート証明書の公開キーの署名に使用される発行されたデジタル証明書です。 クロス証明書は、1 つの信頼されたルート CA から他の複数の Ca への信頼チェーンを作成するための手段を提供します。

で Windows、クロス証明書。

-   1 つの信頼された Microsoft root 権限を持つオペレーティング システムのカーネルを使用できます。
-   ソフトウェア発行元証明書を発行 (SPCs)、コード署名に使用される複数の商用 Ca を信頼チェーンを拡張するソフトウェアの配布、インストール、および Windows での読み込み

ここではクロス証明書は、カーネル モードのソフトウェアを適切に署名するために、Windows Driver Kit (WDK) のコード署名ツールで使用されます。 カーネル モードのソフトウェアにデジタル署名は、Windows 用にパブリッシュされているすべてのソフトウェアのコード署名に似ています。 クロス証明書は、カーネル モードのソフトウェアのサインイン時に、開発者またはソフトウェアの発行元によってデジタル署名に追加されます。 バイナリ ファイルまたはカタログのデジタル署名をコード署名ツールで、クロス証明書自体が追加されます。

**適切なクロス証明書を選択します。**

Microsoft では、カーネル モード コードのコード署名の SPCs を発行する各 CA に対して特定の間の証明書を提供します。 クロス証明書の詳細については、[カーネル モード コード署名用クロス証明書](cross-certificates-for-kernel-mode-code-signing.md)を参照してください。 このトピックのリスト、Microsoft の名前は、CA ベンダーと、適切なクロス証明書、SPC を発行したルート証明機関の権限。 CA ベンダーによって発行された SPC 用の適切なクロス証明を見つけて、クロス証明書を署名するには、リリースを使用し、ドライバー ディレクトリに保存は、署名のコンピューターにダウンロードします。 署名のいずれかのコマンドで使用する場合、この証明書に絶対パスを提供することをお勧めします。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>個人証明書ストアに SPC 情報をインストールします。


*抜粋をさらに*[ソフトウェア発行元証明書](software-publisher-certificate.md):

準拠している方法でドライバーの署名に、SPC を使用するために、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)、Personal Information Exchange 証明書の情報を含める必要がありますはまず (*.pfx*)ファイルです。 含まれている情報、 *.pfx*ドライバーに署名するローカル コンピューターの個人証明書ストアにファイルを追加し、必要があります。

CA が発行する可能性があります、 *.pfx*必要な証明書情報を含むファイル。 そのため、追加できる場合、します。*pfx*ファイルで説明されている手順に従って個人証明書ストアを[個人用証明書ストアに .pfx ファイルをインストールする](software-publisher-certificate.md#installing-a-pfx-file-in-the-personal-certificate-store)します。

ただし、CA は、次のファイルのペアを発行する可能性があります。

-   A *.pvk*秘密キーの情報を含むファイル。

-   *.Spc*または *.cer*公開キー情報を含むファイル。

この場合、ファイルのペア (、 *.pvk*と *.spc、* または *.pvk*と *.cer*) に変換する必要があります、 *.pfx*個人証明書ストアに証明書情報を追加するにはファイル。

作成します。*pfx* CA によって発行されたファイルのペアからファイルを次の手順に従います。

-   変換する、 *.pvk*ファイルと *.spc*ファイルを *.pfx*ファイルで、次を使用して、 [ **Pvk2Pfx** ](https://msdn.microsoft.com/library/windows/hardware/ff550672)コマンド プロンプトでコマンド:

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   変換する、 *.pvk*ファイルと *.cer*ファイルに、 *.pfx*ファイルで、コマンド プロンプトで次の Pvk2Pfx コマンドを使用します。

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

使用されるパラメーターを以下に示します、 [ **Pvk2Pfx** ](https://msdn.microsoft.com/library/windows/hardware/ff550672)コマンド。

-   **- Pvk**  *mypvkfile.pvk*パラメーターを指定します、 *.pvk*ファイル。

-   **-Pi**  *mypvkpassword*オプションのパスワードを指定します *。pvk*ファイル。

-   **- Spc** *myspcfile.spc*パラメーターを指定します、 *.spc*ファイルまたは **- spc**  *mycerfile.cer*パラメーターを指定します、 *.cer*ファイル。

-   **- Pfx** *mypfxfile.pfx*オプションの名前を指定する *.pfx*ファイル。

-   **Po** *pfxpassword*オプションのパスワードを指定します、 *.pfx*ファイル。

-   **-F**オプション構成を置き換える既存の Pvk2Pfx *.pfx*ファイルが存在する場合。

**重要な**  強力なパスワードを pvk と pfx ファイルを保護する必要があります。

 

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>個人用証明書ストアに .pfx ファイルをインストールします。


署名のカーネル モード用には、ドライバーでは、証明書およびキー、.pfx ファイルに格納されているをローカルの個人証明書ストアにインポートする必要があります。 Signtool はカーネル モード ドライバーの署名の .pfx ファイルの使用をサポートしていません。 .Pfx ファイルから証明書を使用しているときにシグネチャでクロス証明書を追加することで競合が原因の制限は、します。

*抜粋です最終*[ソフトウェア発行元証明書](software-publisher-certificate.md):。

取得した後、 *.pfx* 、CA からファイルや作成、 *.pfx*からファイルを *.pvk* 、どちらか、 *。spc*または *.cer*ファイルに、追加の情報、 *.pfx*ドライバーに署名するローカル コンピューターの個人証明書ストアにファイル。 内の情報をインポートする証明書のインポート ウィザードを使用することができます、 *.pfx*個人証明書ストアに次のようにファイルします。

1.  検索、 *.pfx* Windows エクスプ ローラーでファイルし、ファイルをダブルクリックして、証明書のインポート ウィザードを開きます。

2.  コード署名証明書を個人証明書ストアにインポートする証明書のインポート ウィザードの手順に従います。

*抜粋* [SPC を証明書ストアにインポート](importing-an-spc-into-a-certificate-store.md):

Windows Vista では、インポートする別の方法で始まる、 *.pfx*ファイルをローカルの個人証明書ストアには、 [CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)コマンド ライン ユーティリティです。 次のコマンドライン例をインポートする CertUtil を使用して、 *abc.pfx*個人証明書ストアにファイル。

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

各項目の意味は次のとおりです。

-   **-ユーザー**オプションは、個人用ストアの「現在のユーザー」を指定します。

-   **-P**のパスワードを指定するオプション、 *.pfx*ファイル (*pfxpassword*)。

-   **-Importpfx**オプションの名前を指定します、 *.pfx*ファイル (*abc.pfx*)。

## <a name="view-spc-properties"></a>SPC のプロパティの表示


証明書の MMC スナップイン (certmgr.msc) を使用して、個人証明書ストアに証明書を表示します。

1.  証明書スナップインで、certmgr.msc を起動します。
2.  スナップインの左側のウィンドウで、個人証明書ストアのフォルダーを選択します。
3.  証明書 フォルダーをクリックし、リリースに署名するために使用される証明書をダブルクリックします。
4.  [証明書] ダイアログ ボックスの [詳細] タブには、証明書のサブジェクト名を強調表示するフィールドの一覧からサブジェクトを選択します。 このセクションの例の Signtool の/n 引数で使用される名前です。

## <a name="signing"></a>署名


**基づく**[リリース署名ドライバー パッケージのカタログ ファイル](release-signing-a-driver-package-s-catalog-file.md):

ドライバー パッケージに署名される cat ファイルに署名するには、次のコマンドを実行します。 /N コマンドは、上記の手順 4. で、[件名] に表示されますが、証明書の引用符で囲まれた名前を使用する必要がありますとして CN = MyCompany inc.

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s My /n “MyCompany Inc.“ /t http://timestamp.verisign.com/scripts/timestamp.dll  toaster.cat
```

/ac ファイル名

署名ブロックに追加する追加の証明書を含むファイルを指定します。 これは、クロス署名証明書、MSCV VSClass3.cer、クロス証明書のダウンロード リンク、Microsoft から取得します。 クロス証明書は、現在のディレクトリにない場合は、完全なパス名を使用します。 必須ではありませんが、cat ファイルの署名中にクロス証明書を追加することをお勧めします。

/s StoreName

証明書を検索するときに開くストアを指定します。 このオプションが指定されていない場合、My ストアを開くと、個人証明書ストアであります。

/n SubjectName

署名証明書のサブジェクトの名前を指定します。 この値は、サブジェクト名の一部でもかまいません。

/t URL

タイム スタンプ サーバーの URL を指定します。 このオプションが存在しない場合は、タイムスタンプはいない署名付きのファイルにします。 **時刻のタイムスタンプでは、SPC 署名証明書取得の他の理由から取り消されるまでに無期限にで署名されたドライバー パッケージは有効です。**

すべて署名前の手順の説明に従って正しくが従う必要があります、ドライバーの署名できなくのそれ以外の場合。 次に示すエラーが発生する可能性があります。

```cpp
SignTool Error: No certificates were found that met all the given criteria
```

## <a name="embed-signing"></a>署名を埋め込む


**基づく**[埋め込みの署名でのドライバーをリリース署名](release-signing-a-driver-through-an-embedded-signature.md):

Windows Vista では、カーネル モード コード署名では、カーネル モード ドライバーが読み込まれるかどうかをポリシー コントロールを開始しています。 Windows Vista と共に登場した Windows の 64 ビット バージョンでは、Windows の 32 ビット バージョンと比較したより厳しい要件を持ちます。

カーネル モードのブート開始ドライバーは、埋め込みのソフトウェア発行元証明書 (SPC) の署名に必要です。 これは、任意の種類のブート開始ドライバーの PnP または非 PnP カーネル モードに適用されます。 Windows の 32 ビット バージョンにも適用されます。 ブート開始ドライバーが埋め込みの SPC 署名、WHQL リリース署名では、カタログのファイルまたは SPC シグネチャを持つカタログ ファイルのいずれかにいる必要がありますが、PnP カーネル モード ドライバー。

参照してください[カーネル モード コード署名要件](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)の追加情報。

コマンドは、署名 toaster.sys ファイルを埋め込みます。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s my /n “MyCompany Inc. “ /t http://timestamp.verisign.com/scripts/timestamp.dll   toaster.sys
```

署名が完了した後は、署名されたドライバーを確認するには、次のコマンドを実行します。

```cpp
signtool verify  /kp  /v  /c  tstamd64.cat  toastpkg.inf
```

コマンドの出力:

```cpp
Verifying: toaster.inf
File is signed in catalog: toaster.cat
Hash of file (sha1): 580C2A24C3A9E12817E18ADF1C4FE9CF31B01EA3

Signing Certificate Chain:

    Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
    Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
    Expires:   Wed Jul 16 15:59:59 2036
    SHA1 hash: 4EB6D578499B1CCF5F581EAD56BE3D9B6744A5E5

        Issued to: VeriSign Class 3 Code Signing 2010 CA
        Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
        Expires:   Fri Feb 07 15:59:59 2020
        SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

            Issued to: Contoso, Inc
            Issued by: VeriSign Class 3 Code Signing 2010 CA
            Expires:   Thu Dec 04 15:59:59 2014
            SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269

The signature is timestamped: Mon Jan 27 14:48:55 2014
Timestamp Verified by:
    Issued to: Thawte Timestamping CA
    Issued by: Thawte Timestamping CA
    Expires:   Thu Dec 31 15:59:59 2020
    SHA1 hash: BE36A4562FB2EE05DBB3D32323ADF445084ED656

        Issued to: Symantec Time Stamping Services CA - G2
        Issued by: Thawte Timestamping CA
        Expires:   Wed Dec 30 15:59:59 2020
        SHA1 hash: 6C07453FFDDA08B83707C09B82FB3D15F35336B1

            Issued to: Symantec Time Stamping Services Signer - G4
            Issued by: Symantec Time Stamping Services CA - G2
            Expires:   Tue Dec 29 15:59:59 2020
            SHA1 hash: 65439929B67973EB192D6FF243E6767ADF0834E4
Cross Certificate Chain:
    Issued to: Microsoft Code Verification Root
    Issued by: Microsoft Code Verification Root
    Expires:   Sat Nov 01 05:54:03 2025
    SHA1 hash: 8FBE4D070EF8AB1BCCAF2A9D5CCAE7282A2C66B3     
       
 Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
        Issued by: Microsoft Code Verification Root
        Expires:   Mon Feb 22 11:35:17 2021
        SHA1 hash: 57534CCC33914C41F70E2CBB2103A1DB18817D8B
            
            Issued to: VeriSign Class 3 Code Signing 2010 CA
            Issued by: VeriSign Class 3 Public Primary Certification Authority -  G5
            Expires:   Fri Feb 07 15:59:59 2020
            SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

                Issued to: Contoso, Inc
                Issued by: VeriSign Class 3 Code Signing 2010 CA
                Expires:   Thu Dec 04 15:59:59 2014
                SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269

Successfully verified: toaster.inf

Number of files successfully Verified: 1
Number of warnings: 0 
Number of errors: 0
```

Microsoft コードの検証のルートの証明書チェーン内の存在に注意してください。

次に、チェックは toaster.sys ファイルの署名を埋め込みます。

```cpp
signtool verify  /v  /kp  toaster.sys
```

コマンドの出力:

```cpp
Verifying: toaster.sys Hash of file (sha1): CCF5F5C02FEDE87D92FCB7B536DBF5D5EFDB7B41

Signing Certificate Chain:
    Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
    Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
    Expires:   Wed Jul 16 15:59:59 2036
    SHA1 hash: 4EB6D578499B1CCF5F581EAD56BE3D9B6744A5E5

        Issued to: VeriSign Class 3 Code Signing 2010 CA
        Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
        Expires:   Fri Feb 07 15:59:59 2020
        SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

            Issued to: Contoso, Inc
            Issued by: VeriSign Class 3 Code Signing 2010 CA
            Expires:   Thu Dec 04 15:59:59 2014             SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269 
The signature is timestamped: Mon Jan 27 14:48:55 2014 Timestamp Verified by:
    Issued to: Thawte Timestamping CA     Issued by: Thawte Timestamping CA     Expires:   Thu Dec 31 15:59:59 2020     SHA1 hash: BE36A4562FB2EE05DBB3D32323ADF445084ED656 
        Issued to: Symantec Time Stamping Services CA - G2         Issued by: Thawte Timestamping CA         Expires:   Wed Dec 30 15:59:59 2020         SHA1 hash: 6C07453FFDDA08B83707C09B82FB3D15F35336B1 
            Issued to: Symantec Time Stamping Services Signer - G4             Issued by: Symantec Time Stamping Services CA - G2             Expires:   Tue Dec 29 15:59:59 2020             SHA1 hash: 65439929B67973EB192D6FF243E6767ADF0834E4 
Cross Certificate Chain:
    Issued to: Microsoft Code Verification Root     Issued by: Microsoft Code Verification Root     Expires:   Sat Nov 01 05:54:03 2025     SHA1 hash: 8FBE4D070EF8AB1BCCAF2A9D5CCAE7282A2C66B3         
        Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
        Issued by: Microsoft Code Verification Root
        Expires:   Mon Feb 22 11:35:17 2021
        SHA1 hash: 57534CCC33914C41F70E2CBB2103A1DB18817D8B

            Issued to: VeriSign Class 3 Code Signing 2010 CA
            Issued by: VeriSign Class 3 Public Primary Certification Authority -  G5
            Expires:   Fri Feb 07 15:59:59 2020
            SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F 
                Issued to: Contoso, Inc                 Issued by: VeriSign Class 3 Code Signing 2010 CA                 Expires:   Thu Dec 04 15:59:59 2014                 SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269 
Successfully verified: toaster.sys 
Number of files successfully Verified: 1 Number of warnings: 0 Number of errors: 0 
```

ここでも、Microsoft のコードの検証のルートの証明書チェーン内の存在に注意してください。

 

 





