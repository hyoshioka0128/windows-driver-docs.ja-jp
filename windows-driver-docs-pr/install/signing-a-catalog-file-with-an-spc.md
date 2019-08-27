---
title: SPC を使用したカタログ ファイルの署名
description: SPC を使用したカタログ ファイルの署名
ms.assetid: 8fe1fc32-73c9-4c09-96bd-93effb35c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a61c6638f663c6757957a44abdd65fec95da2885
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025301"
---
# <a name="signing-a-catalog-file-with-an-spc"></a>SPC を使用したカタログ ファイルの署名


次の[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)コマンドを使用して、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)を使用してカーネルモード[ドライバーパッケージ](driver-packages.md)の[カタログファイル](catalog-files.md)に署名します。 Windows Vista 以降のバージョンの windows では、 [WHQL リリースシグネチャ](whql-release-signature.md)のないカーネルモードドライバーパッケージは、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)と PnP の両方に準拠するために、SPC 署名を使用して署名されている必要があります。 64 [デバイスのインストール署名の要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.digicert.com CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、カタログファイル*CatalogFileName.cat*に署名するように SignTool を構成します。

-   **/V** verbose オプションは、実行および警告メッセージを出力するように SignTool を構成します。

-   **/Ac** *クロス certificatefile*オプションでは、 *spcisdeleted ename*によって指定されたソフトウェア発行元証明書 (SPC) に関連付けられている証明書の *.cer*ファイルを指定します。

-   **/S** *spccertificatestore*オプションは、 *spcに*よって指定されたソフトウェア発行元証明書を保持する証明書ストアの名前を指定します。 「[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)」で説明されているように、証明書情報は *.pfx*ファイルに含まれている必要があります。また、 *.pfx*ファイル内の情報は、ローカルコンピューターの個人証明書ストアに追加する必要があります。 個人証明書ストアは、 **/s my**というオプションで指定されます。

-   **/N** *Spcは*、 *spccertificatename*証明書ストア内の証明書の名前を指定します。

-   **/T**  *http://timestamp.digicert.com* オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *CatalogFileName.cat*カタログファイルの名前を指定します。

たとえば、次のコマンドは、Personal "my" 証明書ストアの "contoso.com" という名前の*Tstamd64.cat*カタログファイルと、対応するクロス証明書ストアに署名します。 署名は、サービス http://timestamp.digicert.com によってタイムスタンプが付けられます。 この例では、カタログファイルは、コマンドが実行されているディレクトリと同じディレクトリにあります。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.digicert.com tstamd64.cat 
```

 

 





