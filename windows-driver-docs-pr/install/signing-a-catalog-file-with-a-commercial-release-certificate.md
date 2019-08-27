---
title: 商用リリース証明書でのカタログ ファイルの署名
description: 商用リリース証明書でのカタログ ファイルの署名
ms.assetid: 362b0c79-50b9-4749-80e2-62601d76e9e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f42fea9e76753988760af4e1de1e390b3e5aa555
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025302"
---
# <a name="signing-a-catalog-file-with-a-commercial-release-certificate"></a>商用リリース証明書でのカタログ ファイルの署名


次の[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)コマンドを使用して、[商用リリース証明書](commercial-release-certificate.md)を使用してカーネルモード[ドライバーパッケージ](driver-packages.md)の[カタログファイル](catalog-files.md)に署名します。

**32注**  : windows Vista 以降のバージョンの windows では、商用リリース証明書のみを使用して、これらの windows バージョンでリリースされるカーネルモードドライバーに署名することができます。

 

```cpp
SignTool sign /v /s CertificateStore /n CertificateName /t http://timestamp.digicert.com CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、カタログファイル*CatalogFileName.cat*に署名するように SignTool を構成します。

-   **/V** verbose オプションは、実行および警告メッセージを出力するように SignTool を構成します。

-   **/S** *certificatestore*オプションは、指定された*ename*証明書を含む証明書ストアの名前を指定します。 証明書を発行した証明機関 (CA) の指示に従って、システム証明書ストアに証明書をインストールします。

-   **/N**の指定された *ename*オプションは、 *certificatestore*証明書ストア内の証明書の名前を指定します。

-   **/T**   *http://timestamp.digicert.com* オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *CatalogFileName.cat*カタログファイルの名前を指定します。

 

 





