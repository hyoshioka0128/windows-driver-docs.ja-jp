---
title: ソフトウェア発行元証明書
description: ソフトウェア発行元証明書
ms.assetid: eb06c630-9a3d-4f53-b00b-b1254c8bbaec
keywords:
- カタログファイル WDK ドライバー署名、SPC
- ソフトウェア発行元証明書 WDK ドライバー署名
- SPC WDK ドライバー署名
- パブリックリリースドライバー署名 WDK、SPC
- リリース署名 WDK、SPC
- クロス証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b351415e43f1bbfb007153a90ee89e8d0428a11
ms.sourcegitcommit: 55171d00a4d0776ffbea40ab421f765c5432fcaa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995441"
---
# <a name="software-publisher-certificate"></a>ソフトウェア発行元証明書


64ビットバージョンの Windows の[カーネルモードコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠するには、ソフトウェア発行元証明書 (SPC) を使用してカーネルモードドライバーに署名することができます。 SPC は、このような証明書を発行するために Microsoft によって承認されたサードパーティの証明機関 (CA) から取得されます。 この種類の SPC で生成される署名は、64ビット版と32ビット版の Windows の[PnP ドライバー署名要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)にも準拠しています。

**注:**   デスクトップエディションの場合は windows 10 (Home、Pro、Enterprise、および教育) と windows Server 2016 カーネルモードドライバーは windows ハードウェアデベロッパーセンターダッシュボードに署名されている必要があり、windows hardware dev center ダッシュボードには EV が必要です。証明. これらの変更の詳細については、「 [Windows 10 でのドライバー署名の変更点](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)」を参照してください。

 > [!CAUTION] 
 > 2021以降では、クロス証明書の大半が期限切れになります。 これらのクロス証明書が期限切れになると、これらのクロス証明書にチェーンされているコード署名証明書は、新しいカーネルモードデジタル署名を作成できなくなります。 これは、すべてのバージョンの Windows に影響します。 詳細については、「[ソフトウェア発行元証明書と商用リリース証明書の廃止](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)」を参照してください。

## <a name="cross-certificates"></a>クロス証明書

SPC を取得するだけでなく、Microsoft によって発行されたクロス証明書を取得する必要があります。 クロス証明書は、SPC を発行した CA が信頼されたルート証明機関であることを確認するために使用されます。 クロス証明書は、別の CA のルート証明書の公開キーに署名する CA によって発行された x.509 証明書です。 クロス証明書を使用すると、システムは1つの信頼された Microsoft ルート証明機関を持つことができますが、SPCs を発行する商用 Ca に対して信頼チェーンを柔軟に拡張することもできます。

発行元は、[ドライバーパッケージ](driver-packages.md)を使用してクロス証明書を配布する必要はありません。 クロス証明書は、ドライバーパッケージの[カタログファイル](catalog-files.md)のデジタル署名、またはドライバーファイルに埋め込まれている署名に含まれています。 ドライバーパッケージをインストールするユーザーは、クロス証明書の使用によって発生する追加の構成手順を実行する必要はありません。

SPCs を提供する証明機関の一覧と、クロス証明書の詳細については、「[カーネルモードコード署名用のクロス証明書](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)」を参照してください。 証明機関の web サイトに記載されている手順に従って、ドライバーの署名に使用するコンピューターで SPC とそれに対応するクロス証明書を取得してインストールする方法について説明します。 また、ドライバーに署名するローカルコンピューターの個人証明書ストアに SPC 情報を追加する必要があります。 この要件の詳細については、「[個人証明書ストアに SPC 情報をインストール](#installing-spc-information-in-the-personal-certificate-store)する」を参照してください。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>個人証明書ストアに SPC 情報をインストールする

SPC を使用して、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠した方法でドライバーに署名するには、まず、証明書情報が Personal information Exchange ( *.pfx*) ファイルに含まれている必要があります。 *.Pfx*ファイルに含まれる情報は、ドライバーに署名するローカルコンピューターの個人証明書ストアに追加する必要があります。

CA は、必要な証明書情報を含む *.pfx*ファイルを発行する場合があります。 その場合は、を追加できます。「[個人証明書ストアに .Pfx ファイルをインストール](#installing-a-pfx-file-in-the-personal-certificate-store)する」で説明されている手順に従って、 *Pfx*ファイルを個人証明書ストアに保存します。

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

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>個人証明書ストアに .pfx ファイルをインストールする

CA から *.pfx*ファイルを取得した後、または *.pvk*とのどちらかから *.pfx*ファイルを作成した場合。*spc*ファイルまたは *.cer*ファイル。 *.pfx*ファイル内の情報を、ドライバーに署名するローカルコンピューターの個人証明書ストアに追加します。 証明書のインポートウィザードを使用して、次のように *.pfx*ファイル内の情報を個人用証明書ストアにインポートできます。

1.  Windows エクスプローラーで *.pfx*ファイルを見つけ、ファイルをダブルクリックして、証明書のインポートウィザードを開きます。

2.  証明書のインポートウィザードの手順に従って、コード署名証明書を個人証明書ストアにインポートします。


 





