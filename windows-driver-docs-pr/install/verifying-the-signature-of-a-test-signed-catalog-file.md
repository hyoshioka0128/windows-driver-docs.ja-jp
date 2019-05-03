---
title: テスト署名されたカタログ ファイルの署名の検証
description: テスト署名されたカタログ ファイルの署名の検証
ms.assetid: fa627f5b-977e-49ca-b099-358ed686eef7
keywords:
- テスト署名の検証
- テスト署名の確認
- カタログ ファイル WDK ドライバー署名、署名の検証
- テスト署名カタログ ファイル WDK
- テスト証明書検証 WDK
- テスト署名ドライバー パッケージ WDK、カタログ ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e7622aa7d62cb9292ab0bd316a4b9c2e4d58cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339317"
---
# <a name="verifying-the-signature-of-a-test-signed-catalog-file"></a>テスト署名されたカタログ ファイルの署名の検証


確認する、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)によって、有効な署名された[テスト証明書](test-certificates.md)、次を使用して、 [ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)コマンド。

```cpp
SignTool verify /v /pa CatalogFileName.cat
```

ファイルが表示されていることを確認する、[ドライバー パッケージの](driver-packages.md)カタログ ファイルは、次を使用して、テスト証明書によって署名済み、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)コマンド。

```cpp
SignTool verify /v /pa /c CatalogFileName.cat DriverFileName
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、ドライバー パッケージのカタログ ファイルの署名を検証する SignTool を構成します。 *CatalogFileName.cat*またはドライバ ファイル*DriverFileName*します。

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/Pa**オプションは、カタログ ファイルまたはドライバ ファイルの署名が、PnP デバイス インストールの署名の要件に準拠していることを確認する SignTool を構成します。

-   *CatalogFileName.cat*ドライバー パッケージのカタログ ファイルの名前を指定します。

-    ***/C*** *CatalogFileName.cat*オプション ファイルのエントリを含むカタログ ファイルを指定*DriverFileName*します。**

-   *DriverFileName*カタログ ファイルにエントリがあるファイルの名前は、 *CatalogFileName.cat*します。

注意してくださいを SignTool**確認**コマンドがサインインに使用されたテスト証明書を明示的に指定していない、[カタログ ファイル](catalog-files.md)。 検証操作が成功するには、テスト証明書をインストールする必要があります最初、[信頼されたルート証明機関証明書ストア](trusted-root-certification-authorities-certificate-store.md)署名の検証に使用するローカル コンピューターの。 テスト証明書をローカル コンピューターの信頼されたルート証明機関の証明書ストアにインストールする方法の詳細については、次を参照してください。[テスト コンピューターにテスト証明書をインストールする](installing-a-test-certificate-on-a-test-computer.md)します。 インストール手順は、署名のコンピューターとテスト用のコンピューターの両方で同じです。

次のコマンドことを確認するなど、 *Tstamd64.cat*署名 Windows Vista の要件と以降のバージョンの Windows PnP デバイスのインストールに準拠しているテスト署名があります。 この例で*Tstam64.cat*コマンドが実行される同じディレクトリにします。

```cpp
SignTool verify /v /pa tstamd64.cat
```

 

 





