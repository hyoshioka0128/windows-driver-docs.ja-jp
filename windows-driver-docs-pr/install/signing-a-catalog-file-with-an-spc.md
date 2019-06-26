---
title: SPC を使用したカタログ ファイルの署名
description: SPC を使用したカタログ ファイルの署名
ms.assetid: 8fe1fc32-73c9-4c09-96bd-93effb35c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f291bc2a2f2973c7f250f5cb405e6bb60602b715
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373486"
---
# <a name="signing-a-catalog-file-with-an-spc"></a>SPC を使用したカタログ ファイルの署名


次を使用して、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)に署名するコマンド、[カタログ ファイル](catalog-files.md)カーネル モードの[ドライバー パッケージ](driver-packages.md)で、 [ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)します。 64 ビット バージョンの Windows Vista および以降のバージョンの Windows では、カーネル モード ドライバー パッケージがない、 [WHQL リリース署名](whql-release-signature.md)両方に準拠する SPC 署名を使って署名する必要があります、[カーネル モード コード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)と[PnP デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)します。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドでは、カタログ ファイルに署名する署名ツールを構成します。 *CatalogFileName.cat*します。

-   **/V** /verbose オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Ac** *CrossCertificateFile*オプションは、クロス証明書を指定します *.cer*がソフトウェア発行元証明書 (SPC) に関連付けられているファイル指定された*SPCCertificateName*します。

-   **/S** *SPCCertificateStore*オプションで指定されているソフトウェアの発行元証明書を保持する証明書ストアの名前を指定*SPCCertificateName*. 」の説明に従って[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)、証明書の情報を含める必要があります *.pfx*ファイル、および内の情報、 *.pfx*ファイルである必要がありますローカル コンピューターの個人証明書ストアに追加されます。 個人証明書ストアが、オプションで指定された **/s 自分**します。

-   **/N** *SPCCertificateName*オプションで証明書の名前を指定、 *SPCCertificateStore*証明書ストア。

-   **/T**  * http://timestamp.verisign.com/scripts/timstamp.dll *オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *CatalogFileName.cat*カタログ ファイルの名前を指定します。

たとえば、次のコマンドを記号、 *Tstamd64.cat* SPC とカタログ ファイルは、"my"証明書ストアと対応するクロス証明書に、個人で"contoso.com"をという名前*Rsacertsvrcross.cer*. 署名は、サービスによってタイムスタンプ http://timestamp.verisign.com/scripts/timstamp.dll します。 この例では、カタログ ファイルは、コマンドが実行される同じディレクトリには。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat 
```

 

 





