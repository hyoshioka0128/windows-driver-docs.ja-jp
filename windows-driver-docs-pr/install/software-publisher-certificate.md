---
title: ソフトウェア発行元証明書
description: ソフトウェア発行元証明書
ms.assetid: eb06c630-9a3d-4f53-b00b-b1254c8bbaec
keywords:
- カタログ ファイル WDK ドライバーの署名、SPC
- ソフトウェア発行元証明書の WDK ドライバーの署名
- SPC WDK ドライバーの署名
- パブリック リリース ドライバーの WDK、SPC の署名
- WDK、SPC が署名をリリースします。
- クロス証明書の WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 958e6034fcf23c6c0027dfcc541905bf62758666
ms.sourcegitcommit: a678a339f09fbd56a3a6124c0fe86194fedb2ed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "57560609"
---
# <a name="software-publisher-certificate"></a>ソフトウェア発行元証明書


準拠する、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md) Windows の 64 ビット バージョンのソフトウェア発行元証明書 (SPC) を使用して、カーネル モード ドライバーに署名することができます。 SPC は、マイクロソフトがこのような証明書を発行する権限を持つサード パーティ証明機関 (CA) から取得されます。 この種類の SPC 生成された署名にも準拠して、 [PnP ドライバーの署名要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)の 64 ビットと 32 ビット バージョンの Windows。

**注**  デスクトップ エディション (Home、Pro、Enterprise、および Education) および Windows Server 2016 カーネル モード ドライバー用の Windows 10 は Windows ハードウェア デベロッパー センター ダッシュ ボード Windows ハードウェア デベロッパー センター ダッシュ ボードを署名する必要がありますEV 証明書が必要です。 これらの変更に関する詳細については、次を参照してください。 [Windows 10 でドライバー署名の変更](http://blogs.msdn.com/b/windows_hardware_certification/archive/2015/04/01/driver-signing-changes-in-windows-10.aspx)します。

 

### <a name="cross-certificates"></a>クロス証明書

SPC を入手すると、だけでなく、クロス証明書は Microsoft によって発行されるを取得する必要があります。 クロス証明書は、SPC を発行した CA が信頼されたルート機関であることを確認に使用されます。 クロス証明書は、別の CA のルート証明書の公開キーを署名する CA によって発行された X.509 証明書です。 クロス証明書は、単一信頼された Microsoft ルート機関、SPCs を発行する商用の Ca を信頼チェーンを拡張する柔軟性も備えていて、システムを許可します。

発行元をクロス証明書を配布する必要はありません、[ドライバー パッケージ](driver-packages.md)します。 クロス証明書は、ドライバー パッケージのデジタル署名に含まれている[カタログ ファイル](catalog-files.md)またはドライバーのファイルに埋め込まれている署名します。 ドライバー パッケージをインストールするユーザーは、クロス証明書の使用による追加の構成手順を実行する必要はありません。

SPCs を提供する証明機関の一覧については、およびクロス証明書の詳細については、「[カーネル モード コード署名用クロス証明書](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)します。 証明機関の web サイトを取得して、ドライバーに署名するコンピューターに、SPC と対応するクロス証明書をインストールする方法の手順に従います。 さらに、ドライバーに署名するローカル コンピューターの個人証明書ストアには、SPC 情報を追加する必要があります。 この要件については、次を参照してください。、 [SPC 情報を個人証明書ストアにインストール](#installing-spc-information-in-the-personal-certificate-store)します。

### <a name="installing-spc-information-in-the-personal-certificate-store"></a>個人証明書ストアに SPC 情報をインストールします。

準拠している方法でドライバーの署名に、SPC を使用するために、[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)、Personal Information Exchange 証明書の情報を含める必要がありますはまず (*.pfx*)ファイルです。 含まれている情報、 *.pfx*ドライバーに署名するローカル コンピューターの個人証明書ストアにファイルを追加し、必要があります。

CA が発行する可能性があります、 *.pfx*必要な証明書情報を含むファイル。 そのため、追加できる場合、します。*pfx*ファイルで説明されている手順に従って個人証明書ストアを[個人用証明書ストアに .pfx ファイルをインストールする](#installing-a--pfx-file-in-the-personal-certificate-store)します。

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

### <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>個人用証明書ストアに .pfx ファイルをインストールします。

取得した後、 *.pfx* 、CA からファイルや作成、 *.pfx*からファイルを *.pvk* 、どちらか、 *。spc*または *.cer*ファイルに、追加の情報、 *.pfx*ドライバーに署名するローカル コンピューターの個人証明書ストアにファイル。 内の情報をインポートする証明書のインポート ウィザードを使用することができます、 *.pfx*個人証明書ストアに次のようにファイルします。

1.  検索、 *.pfx* Windows エクスプ ローラーでファイルし、ファイルをダブルクリックして、証明書のインポート ウィザードを開きます。

2.  コード署名証明書を個人証明書ストアにインポートする証明書のインポート ウィザードの手順に従います。


 





