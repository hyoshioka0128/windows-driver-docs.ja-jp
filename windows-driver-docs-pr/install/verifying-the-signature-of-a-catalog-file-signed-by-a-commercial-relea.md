---
title: 商用の証明書によって署名カタログ ファイルを確認します。
description: 商用リリース証明書で署名されたカタログ ファイルの署名の検証
ms.assetid: 153bb1e7-009d-4ef8-b5d7-a9e6eecf65bf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1780998634cbbe23211e080ef8c6012fdd1512b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339305"
---
# <a name="verifying-the-signature-of-a-catalog-file-signed-by-a-commercial-release-certificate"></a>商用リリース証明書で署名されたカタログ ファイルの署名の検証


確認する、[カタログ ファイル](catalog-files.md)によって、有効な署名が[コマーシャル リリースの証明書](commercial-release-certificate.md)、次を使用して、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)コマンド。

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

確認するに記載されているファイル、[ドライバー パッケージの](driver-packages.md)カタログ ファイルが有効な商用リリース証明書によって署名された、SignTool の次のコマンドを使用します。

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、ドライバー パッケージのカタログ ファイルの署名を検証する SignTool を構成します。 *CatalogFileName.cat*またはドライバ ファイル*DriverFileName*します。

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Pa**オプションは、カタログ ファイルまたはドライバ ファイルの署名が PnP ドライバーのインストール要件に準拠していることを確認する SignTool を構成します。

-   *CatalogFileName.cat*ドライバー パッケージのカタログ ファイルの名前を指定します。

-    ***/C*** *CatalogFileName.cat*オプション ファイルのエントリを含むカタログ ファイルを指定*DriverFileName*します。**

-   *DriverFileName*カタログ ファイルにエントリがあるファイルの名前を示す*CatalogFileName.cat*します。

 

 





