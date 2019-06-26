---
title: カタログ ファイルのテスト署名
description: カタログ ファイルのテスト署名
ms.assetid: a6397f8f-e5f1-4ce2-af7b-a7846fa30bc8
keywords:
- カタログ ファイル WDK ドライバーの署名、署名のテスト
- テスト署名カタログ ファイル WDK
- テスト署名ドライバー パッケージ WDK、カタログ ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b235ab765e83ccbb2ac4b8e991efc7b87ead6a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377236"
---
# <a name="test-signing-a-catalog-file"></a>カタログ ファイルのテスト署名


作成することを確認したら、[ドライバー パッケージの](driver-packages.md) [カタログ ファイル](catalog-files.md)を使用して、 [ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)テスト署名カタログ ファイル」の説明に従って、次のトピック:

[MakeCert テスト証明書またはテスト署名の市販のテスト証明書のドライバー パッケージのカタログ ファイルを使用します。](#using-a-makecert-test-certificate-or-commercial-test-certificate-to-te)

[テストへの署名をエンタープライズ CA テスト証明書のドライバー パッケージのカタログ ファイルを使用します。](#using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-)

### <a href="" id="using-a-makecert-test-certificate-or-commercial-test-certificate-to-te"></a> MakeCert テスト証明書またはテスト署名証明書を市販のテストのドライバー パッケージのカタログ ファイルを使用します。

次の SignTool コマンドを使用して、サインイン、[カタログ ファイル](catalog-files.md)を使用して、 [MakeCert テスト証明書](makecert-test-certificate.md)または[市販のテスト証明書](commercial-test-certificate.md):

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドは、SignTool のアクセスを構成、[カタログ ファイル](catalog-files.md)という*CatalogFileName.cat*します。

-   **/V** /verbose オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/S** *TestCertStoreName*オプションという名前のテスト証明書を含むテスト証明書ストアの名前を提供する*TestCertName*します。

-   **/N** *TestCertName*オプションという名前の証明書ストアにインストールされているテスト証明書の名前を提供する*TestCertStoreName*します。 テスト証明書には、MakeCert テスト証明書または市販のテスト証明書のいずれかを指定できます。

-   **/T**  * http://timestamp.verisign.com/scripts/timstamp.dll *オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *CatalogFileName.cat*の名前を指定します、[カタログ ファイル](catalog-files.md)します。

次のコマンドは、SignTool を使用して、テスト署名する方法を示しています、[ドライバー パッケージの](driver-packages.md)カタログ ファイル。 この例は、カタログ ファイルを署名*Tstamd64.cat*コマンドが実行される同じディレクトリにあります。 テスト証明書の名前は"contoso.com(test)""PrivateCertStore"という名前の証明書ストアにインストールされています。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-"></a> ドライバー パッケージのカタログ ファイルのテストへの署名をエンタープライズ CA テスト証明書を使用

次の SignTool コマンドでは、エンタープライズ CA が、テストへの署名を使用したテスト証明書を発行する前提としています、[ドライバー パッケージ](driver-packages.md)します。 場合、[テスト証明書をエンタープライズ CA](enterprise-ca-test-certificate.md) 、証明書ストアに存在する唯一のテスト証明書は、次のコマンドを使用できますのみ指定する、 **/a**オプションとの名前、[カタログ ファイル](catalog-files.md)します。 このような状況では、SignTool は検索し、既定では、エンタープライズ CA テスト証明書を使用します。

エンタープライズ CA のテスト証明書だけでなく他のテスト証明書を取得または作成した場合は、SignTool オプションを使用する必要があります **/s**と **/n**テスト証明書ストアの名前を指定してテスト証明書ストアにインストールされているテスト証明書の名前。

```cpp
SignTool sign /v /a /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

 

 





