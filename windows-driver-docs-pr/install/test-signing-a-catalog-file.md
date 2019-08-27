---
title: カタログ ファイルのテスト署名
description: カタログ ファイルのテスト署名
ms.assetid: a6397f8f-e5f1-4ce2-af7b-a7846fa30bc8
keywords:
- カタログファイル WDK ドライバー署名、テスト署名
- 署名カタログファイルのテスト WDK
- テスト署名ドライバーパッケージ WDK、カタログファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70caf48f50cadf12d53ebc642c77e01ad8f60923
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025346"
---
# <a name="test-signing-a-catalog-file"></a>カタログ ファイルのテスト署名


[ドライバーパッケージの](driver-packages.md) [カタログファイル](catalog-files.md)を作成して確認したら、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用して、次のトピックの説明に従って、カタログファイルに対するテスト署名を行います。

[MakeCert テスト証明書または商用テスト証明書を使用して、ドライバーパッケージのカタログファイルのテスト署名を行う](#using-a-makecert-test-certificate-or-commercial-test-certificate-to-te)

[エンタープライズ CA テスト証明書を使用して、ドライバーパッケージのカタログファイルのテスト署名を行う](#using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-)

### <a href="" id="using-a-makecert-test-certificate-or-commercial-test-certificate-to-te"></a>MakeCert テスト証明書または商用テスト証明書を使用して、ドライバーパッケージのカタログファイルのテスト署名を行う

[MakeCert テスト](makecert-test-certificate.md)証明書または[商用テスト証明書](commercial-test-certificate.md)を使用して[カタログファイル](catalog-files.md)に署名するには、次の SignTool コマンドを使用します。

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.digicert.com CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、 *CatalogFileName.cat*という名前の[カタログファイル](catalog-files.md)に署名するように SignTool を構成します。

-   **/V** verbose オプションは、実行および警告メッセージを出力するように SignTool を構成します。

-   **/S** *TestCertStoreName*オプションは、 *testcertname*という名前のテスト証明書を含むテスト証明書ストアの名前を指定します。

-   **/N** *testcertname*オプションは、 *TestCertStoreName*という名前の証明書ストアにインストールされているテスト証明書の名前を指定します。 テスト証明書には、MakeCert テスト証明書または商用テスト証明書のいずれかを指定できます。

-    */T http://timestamp.digicert.com* オプションは、DigiCert が提供するパブリックに使用できるタイムスタンプサーバーの URL を指定します。

-   *CatalogFileName.cat* [カタログファイル](catalog-files.md)の名前を指定します。

次のコマンドは、SignTool を使用して、[ドライバーパッケージの](driver-packages.md)カタログファイルをテスト署名する方法を示しています。 この例では、コマンドが実行されているディレクトリにある、カタログファイル*Tstamd64.cat*に署名します。 テスト証明書の名前は "contoso .com (test)" で、"PrivateCertStore" という名前の証明書ストアにインストールされています。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.digicert.com tstamd64.cat
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-test-sign-a-driver-package-"></a>エンタープライズ CA テスト証明書を使用して、ドライバーパッケージのカタログファイルのテスト署名を行う

次の SignTool コマンドは、エンタープライズ CA が[ドライバーパッケージ](driver-packages.md)のテスト署名に使用するテスト証明書を発行することを前提としています。 [エンタープライズ CA テスト証明書](enterprise-ca-test-certificate.md)が証明書ストアに存在する唯一のテスト証明書である場合は、次のコマンドを使用できます。ここでは、 **/a**オプションと[カタログファイル](catalog-files.md)の名前のみを指定します。 この場合、SignTool は既定でエンタープライズ CA テスト証明書を検索して使用します。

エンタープライズ CA テスト証明書に加えて他のテスト証明書を作成または取得した場合は、SignTool オプション **/s**と **/n**を使用して、テスト証明書ストアの名前とテスト証明書の名前を指定する必要があります。テスト証明書ストアにインストールされます。

```cpp
SignTool sign /v /a /t http://timestamp.digicert.com CatalogFileName.cat
```

 

 





