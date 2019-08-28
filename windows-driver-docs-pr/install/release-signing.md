---
title: リリース署名
description: テスト署名を完了し、ドライバーがリリース可能であることを確認した後、ドライバーパッケージをリリース署名する必要があります。 ドライバーパッケージに署名する方法は2つあります。
ms.assetid: 71499A0A-95D0-411C-84D1-C4B91FA4E6B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6d18ca5172ccb1159c9615229f5a675b0506dd
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063934"
---
# <a name="release-signing"></a>リリース署名


テスト署名を完了し、ドライバーがリリース可能であることを確認した後、ドライバーパッケージをリリース署名する必要があります。 ドライバーパッケージに署名する方法は2つあります。

リリース署名は、Windows Vista 以降のバージョンの Windows に読み込まれるカーネルモードまたはユーザーモードのバイナリ (たとえば、.sys ファイルまたは .dll ファイル) の発行元を識別します。

カーネルモードバイナリは、次のいずれかの方法でリリース署名されます。

1.  Windows Hardware Quality Lab (Winqual とも呼ばれます) は、ドライバーパッケージに署名するためのものです。 WHQL リリース署名は、Windows 認定プログラムを通じて取得されます。 次のリンクでは、Windows 認定プログラムの開始から終了までの5つの手順について説明しています。 このオプションの詳細については、「 [Windows ハードウェア認定: ここから開始](https://docs.microsoft.com/previous-versions/hh833792(v=msdn.10))する」を参照してください。 上記のリンクの手順に関する質問は、エイリアスに<sysdev@microsft.com>リダイレクトする必要があります。
2.  ドライバーパッケージは、WHQL プログラムを使用する代わりに、ドライバーの開発者とベンダーによって署名されたリリースにすることができます。 このプログラムは、Vista OS リリースから開始されました。 リリース署名は、ソフトウェア発行元証明書 (SPC) を使用して作成されます。 SPC は、このような証明書を発行するために Microsoft によって承認されたサードパーティの証明機関 (CA) から取得されます。 この種類の SPC で生成される署名は、Windows Vista 以降のバージョンの windows では、64ビット版と32ビット版の PnP ドライバーの署名要件に準拠しています。

次に、メソッド2のドライバーパッケージをリリースするために必要な手順について説明します。

## <a name="obtain-a-software-publisher-certificate-spc"></a>ソフトウェア発行元証明書 (SPC) を取得する


リリース署名には、商用 CA からソフトウェア発行元証明書 (SPC) とも呼ばれるコード署名証明書が必要です。

「[カーネルモードのクロス証明書のコード署名](cross-certificates-for-kernel-mode-code-signing.md)」トピックでは、Microsoft によって承認された商用サードパーティ証明機関 (CA) の一覧を示します。 一覧表示されている CA ベンダーを使用して、ドライバーパッケージをリリースするソフトウェア発行元証明書 (SPC) を提供する必要があります。

CA の指示に従って、SPC を取得し、署名コンピューターに秘密キーをインストールします。 SPC は、ドライバーパッケージに署名するために要求したドライバーベンダーの専用のインストルメントであることに注意してください。 SPC、秘密キー、およびパスワードは、要求元のベンダーの組織外のユーザーと共有することはできません。

## <a name="cross-certificates"></a>クロス証明書


*抜粋*[ソフトウェア発行元証明書](software-publisher-certificate.md):

SPC を取得するだけでなく、Microsoft によって発行されたクロス証明書を取得する必要があります。 クロス証明書は、SPC を発行した CA が信頼されたルート証明機関であることを確認するために使用されます。 クロス証明書は、別の CA のルート証明書の公開キーに署名する CA によって発行された x.509 証明書です。 クロス証明書を使用すると、システムは1つの信頼された Microsoft ルート証明機関を持つことができますが、SPCs を発行する商用 Ca に対して信頼チェーンを柔軟に拡張することもできます。

発行元は、[ドライバーパッケージ](driver-packages.md)を使用してクロス証明書を配布する必要はありません。 クロス証明書は、ドライバーパッケージの[カタログファイル](catalog-files.md)のデジタル署名、またはドライバーファイルに埋め込まれている署名に含まれています。 ドライバーパッケージをインストールするユーザーは、クロス証明書の使用によって発生する追加の構成手順を実行する必要はありません。

*選択された抜粋の開始*[カーネルモードコード署名用のクロス証明書](cross-certificates-for-kernel-mode-code-signing.md):

クロス証明書は、ある証明機関 (CA) によって発行されたデジタル証明書であり、別の証明機関のルート証明書の公開キーに署名するために使用されます。 クロス証明書は、単一の信頼されたルート CA から他の複数の Ca への信頼チェーンを作成するための手段を提供します。

Windows では、クロス証明書:

-   オペレーティングシステムのカーネルに、信頼された1つの Microsoft ルート機関を与えることを許可します。
-   ソフトウェア発行元証明書 (SPCs) を発行する複数の商用 Ca に信頼チェーンを拡張します。これは、Windows での配布、インストール、および読み込みのためにコード署名ソフトウェアに使用されます。

ここで提供されているクロス証明書は、カーネルモードソフトウェアに適切に署名するための Windows Driver Kit (WDK) コード署名ツールと共に使用されます。 カーネルモードソフトウェアのデジタル署名は、Windows 向けに発行されたソフトウェアのコード署名に似ています。 クロス証明書は、カーネルモードソフトウェアに署名するときに、開発者またはソフトウェア発行者によってデジタル署名に追加されます。 クロス証明書自体は、バイナリファイルまたはカタログのデジタル署名にコード署名ツールによって追加されます。

**正しいクロス証明書を選択しています**

Microsoft では、コード署名カーネルモードコード用に SPCs を発行する CA ごとに、特定のクロス証明書を提供しています。 クロス証明書の詳細については、「[カーネルモードコード署名のクロス証明書](cross-certificates-for-kernel-mode-code-signing.md)」を参照してください。 このトピックでは、Microsoft が承認した CA ベンダーの名前と、SPC を発行したルート証明機関の正しいクロス証明書の一覧を示します。 CA ベンダーによって発行された SPC の正しいクロス証明書を見つけ、リリース署名に使用する署名コンピューターにクロス証明書をダウンロードして、ドライバーディレクトリに保存します。 任意の署名コマンドで使用する場合は、この証明書への絶対パスを指定することをお勧めします。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>個人証明書ストアに SPC 情報をインストールする


その*他の抜粋*[ソフトウェア発行元証明書](software-publisher-certificate.md):

SPC を使用して、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠した方法でドライバーに署名するには、まず、証明書情報が Personal information Exchange ( *.pfx*) ファイルに含まれている必要があります。 *.Pfx*ファイルに含まれる情報は、ドライバーに署名するローカルコンピューターの個人証明書ストアに追加する必要があります。

CA は、必要な証明書情報を含む *.pfx*ファイルを発行する場合があります。 その場合は、を追加できます。「[個人証明書ストアに .Pfx ファイルをインストール](software-publisher-certificate.md#installing-a-pfx-file-in-the-personal-certificate-store)する」で説明されている手順に従って、 *Pfx*ファイルを個人証明書ストアに保存します。

ただし、CA は次のようなファイルのペアを発行する場合があります。

-   秘密キーの情報を含む *.pvk ファイル。*

-   公開キー情報を格納している *.spc*ファイルまたは *.cer*ファイル。

この場合、証明書情報を個人証明書ストアに追加するには、ファイルのペア ( *.pvk*と *.spc、* または *.pvk*と *.cer*) を *.pfx*ファイルに変換する必要があります。

を作成する場合は。CA によって発行されたファイルのペアからの*pfx*ファイル。次の手順に従います。

-   *.Pvk*ファイルと *.spc*ファイルを *.pfx*ファイルに変換するには、コマンドプロンプトで次の[**Pvk2Pfx**](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)コマンドを使用します。

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   *.Pvk*ファイルと *.cer*ファイルを *.pfx*ファイルに変換するには、コマンドプロンプトで次の Pvk2Pfx コマンドを使用します。

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

次に、 [**Pvk2Pfx**](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)コマンドで使用されるパラメーターについて説明します。

-   **-.Pvk**  *mypvkfile.* .pvk パラメーターには、 *.pvk*ファイルを指定します。

-   **-Pi**  *mypvkpassword*オプションでは、のパスワードを指定します。 *.pvk*ファイル。

-   **-Spc** *myspcfile*は、 *.spc*ファイルまたは **-spc**  *myspcfile を指定します。 .cer*パラメーターは *.cer*ファイルを指定します。

-   **-Pfx** *mypfxfile .pfx*オプションでは、 *.pfx*ファイルの名前を指定します。

-   **-Po** *pfxpassword*オプションは、 *.pfx*ファイルのパスワードを指定します。

-   **-F**オプションは、既存の *.pfx*ファイルが存在する場合に置き換えるように Pvk2Pfx を構成します。

**重要強力な**パスワードを使用して、.pvk ファイルと pfx ファイルを保護する必要があります。  

 

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>個人証明書ストアに .pfx ファイルをインストールする


カーネルモードドライバーに署名する場合は、.pfx ファイルに格納されている証明書とキーをローカルの個人証明書ストアにインポートする必要があります。 Signtool は、カーネルモードドライバーの署名に .pfx ファイルを使用することをサポートしていません。 .Pfx ファイルから証明書を使用しているときに、署名にクロス証明書を追加する際の競合が原因であるという制限があります。

*最終的な抜粋*[ソフトウェア発行元証明書](software-publisher-certificate.md):

CA から *.pfx*ファイルを取得した後、または *.pvk*とのどちらかから *.pfx*ファイルを作成した場合。*spc*ファイルまたは *.cer*ファイル。 *.pfx*ファイル内の情報を、ドライバーに署名するローカルコンピューターの個人証明書ストアに追加します。 証明書のインポートウィザードを使用して、次のように *.pfx*ファイル内の情報を個人用証明書ストアにインポートできます。

1.  Windows エクスプローラーで *.pfx*ファイルを見つけ、ファイルをダブルクリックして、証明書のインポートウィザードを開きます。

2.  証明書のインポートウィザードの手順に従って、コード署名証明書を個人証明書ストアにインポートします。

*抜粋*[SPC を証明書ストアにインポートするに](importing-an-spc-into-a-certificate-store.md)は、次のようにします。

Windows Vista 以降では、 *.pfx*ファイルをローカルの個人用証明書ストアにインポートする別の方法として、 [CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)コマンドラインユーティリティを使用できます。 次のコマンドラインの例では、CertUtil を使用して、Personal 証明書ストアに*abc .pfx*ファイルをインポートします。

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

各項目の意味は次のとおりです。

-   **-User**オプションは、"現在のユーザー" の個人用ストアを指定します。

-   **-P**オプションは、 *.pfx*ファイル (*pfxpassword*) のパスワードを指定します。

-   **-Importpfx**オプションでは、 *.pfx*ファイル (*abc .pfx*) の名前を指定します。

## <a name="view-spc-properties"></a>SPC のプロパティの表示


MMC 証明書スナップイン (certmgr.exe) を使用して、個人証明書ストア内の証明書を表示します。

1.  証明書スナップイン (certmgr.exe) を起動します。
2.  スナップインの左側のウィンドウで、[個人] 証明書ストアフォルダーを選択します。
3.  [証明書] フォルダーをクリックし、リリース署名に使用する証明書をダブルクリックします。
4.  [証明書] ダイアログボックスの [詳細] タブで、フィールドの一覧から [件名] を選択し、証明書のサブジェクト名を強調表示します。 これは、このセクションの例で、Signtool の/n 引数と共に使用される名前です。

## <a name="signing"></a>付き


**基準**[ドライバーパッケージのカタログファイルに対するリリース署名](release-signing-a-driver-package-s-catalog-file.md):

次のコマンドを実行して、ドライバーパッケージに署名する cat ファイルに署名します。 /N コマンドでは、上記の手順 4. で [サブジェクト] の下に表示される証明書の引用符で囲まれた名前を使用する必要があります。これは CN = MyCompany Inc. です。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s My /n “MyCompany Inc.“ /t http://timestamp.digicert.com toaster.cat
```

/ac ファイル名

署名ブロックに追加する追加の証明書を含むファイルを指定します。 これは、Microsoft のクロス証明書のダウンロードリンクから取得した、MSCV-VSClass3 のクロス署名証明書です。 クロス証明書が現在のディレクトリにない場合は、完全なパス名を使用します。 必須ではありませんが、cat ファイルに署名するときにクロス証明書を追加することをお勧めします。

/s StoreName

証明書を検索するときに開くストアを指定します。 このオプションが指定されていない場合は、個人用証明書ストアである My ストアが開きます。

/n SubjectName

署名証明書のサブジェクトの名前を指定します。 この値は、サブジェクト名の一部でもかまいません。

/t URL

タイムスタンプサーバーの URL を指定します。 このオプションが指定されていない場合、署名されたファイルにはタイムスタンプが付きません。 **タイムスタンプを使用すると、署名されたドライバーパッケージは、他の理由で SPC 署名証明書が失効するまで無期限に有効のままになります。**

前述のように、すべての署名手順を正しく実行する必要があります。そうしないと、ドライバーに署名することはできません。 次のようなエラーが表示されることがあります。

```cpp
SignTool Error: No certificates were found that met all the given criteria
```

## <a name="embed-signing"></a>署名の埋め込み


**基準**[リリース-埋め込み署名を使用したドライバーの署名](release-signing-a-driver-through-an-embedded-signature.md):

Windows Vista 以降では、カーネルモードのコード署名ポリシーによって、カーネルモードドライバーが読み込まれるかどうかが制御されます。 windows Vista 以降の64ビットバージョンの windows では、windows の32ビットバージョンと比較して、厳しい要件があります。

カーネルモードのブート開始ドライバーには、埋め込みソフトウェア発行元証明書 (SPC) 署名が必要です。 これは、任意の種類の PnP または非 PnP カーネルモードのブート開始ドライバーに適用されます。 は、32ビットバージョンの Windows にも適用されます。 ブート開始ドライバー以外の PnP カーネルモードドライバーには、埋め込まれた SPC 署名、WHQL リリース署名付きのカタログファイル、または SPC 署名付きのカタログファイルのいずれかが必要です。

詳細については、「[カーネルモードコード署名の要件](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)」を参照してください。

トースターファイルに署名するためのコマンドです。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s my /n “MyCompany Inc. “ /t http://timestamp.digicert.com toaster.sys
```

署名が完了したら、次のコマンドを実行して、署名されたドライバーを確認します。

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

証明書チェーンに Microsoft コード検証ルートが存在することに注意してください。

次に、トースターファイルの埋め込み署名を確認します。

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

ここでも、証明書チェーンに Microsoft コード検証ルートが存在することに注意してください。

 

 





