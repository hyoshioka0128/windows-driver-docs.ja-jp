---
title: 商用リリース証明書でのカタログ ファイルの署名
description: 商用リリース証明書でのカタログ ファイルの署名
ms.assetid: 362b0c79-50b9-4749-80e2-62601d76e9e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d26458965ad429b7c5af7c1e20dc0cf3cdda3be3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373497"
---
# <a name="signing-a-catalog-file-with-a-commercial-release-certificate"></a>商用リリース証明書でのカタログ ファイルの署名


次を使用して、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)に署名するコマンド、[カタログ ファイル](catalog-files.md)カーネル モードの[ドライバー パッケージ](driver-packages.md)で、 [証明書の商用リリース](commercial-release-certificate.md)します。

**注**  の 32 ビット バージョンの Windows Vista と以降のバージョンの Windows を製品版の証明書のみを使用して、これらの Windows バージョンにリリースされるカーネル モード ドライバーに署名します。

 

```cpp
SignTool sign /v /s CertificateStore /n CertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドでは、カタログ ファイルに署名する署名ツールを構成します。 *CatalogFileName.cat*します。

-   **/V** /verbose オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/S** *CertificateStore*オプションを含む証明書ストアの名前を指定します、 *CertificateName*証明書。 システムの証明書ストアに証明書をインストールする方法の証明書を発行した証明機関 (CA) の手順に従います。

-   **/N** *CertificateName*オプションで証明書の名前を指定、 *CertificateStore*証明書ストア。

-   **/T**   * http://timestamp.verisign.com/scripts/timstamp.dll *オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *CatalogFileName.cat*カタログ ファイルの名前を指定します。

 

 





