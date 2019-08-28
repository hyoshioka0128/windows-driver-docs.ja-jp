---
title: ドライバー ファイルのテスト署名
description: ドライバー ファイルのテスト署名
ms.assetid: 3d73d632-e910-43e7-a8fd-c78a11df0206
keywords:
- テスト署名ドライバーパッケージ WDK、ドライバーファイル
- テスト署名ドライバーパッケージ WDK、埋め込み署名
- ドライバーファイルに署名を埋め込む (WDK)
- 署名 WDK、埋め込み
- デジタル署名 WDK、埋め込み
- MakeCert テスト証明書 WDK
- 署名ドライバーファイルのテスト WDK
- 商用テスト証明書 WDK
- エンタープライズ CA テスト証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5f789336df1cb15930f150e8911710a99f38792
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063929"
---
# <a name="test-signing-a-driver-file"></a>ドライバー ファイルのテスト署名


[**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用して、次のトピックで説明するように、ドライバーファイルに署名を埋め込みます。

[MakeCert テスト証明書または商用テスト証明書を使用して、テスト署名をドライバーファイルに埋め込む](#using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-)

[エンタープライズ CA テスト証明書を使用して、テスト署名をドライバーファイルに埋め込む](#using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a)

### <a href="" id="using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-"></a>MakeCert テスト証明書または商用テスト証明書を使用して、テスト署名をドライバーファイルに埋め込む

[MakeCert テスト証明](makecert-test-certificate.md)書または[商用テスト証明書](commercial-test-certificate.md)を使用して、ドライバーファイルに署名を埋め込むには、次の SignTool コマンドを使用します。

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.digicert.com DriverFileName.sys
```

各項目の意味は次のとおりです。

-   Sign コマンドは、ドライバーファイル DriverFileName に署名を埋め込むように SignTool を構成します。

-   **/V** verbose オプションは、実行および警告メッセージを出力するように SignTool を構成します。

-   **/S** *TestCertStoreName*オプションは、 *testcertname*という名前のテスト証明書を含むテスト証明書ストアの名前を指定します。

-   **/N** *testcertname*オプションは、 *TestCertStoreName*という名前の証明書ストアにインストールされているテスト証明書の名前を指定します。 テスト証明書には、MakeCert テスト証明書または商用テスト証明書のいずれかを指定できます。

-    */T http://timestamp.digicert.com* オプションは、DigiCert が提供するパブリックに使用できるタイムスタンプサーバーの URL を指定します。

-   *Driverfilename .sys*は、ドライバーファイルの名前です。

次のコマンドは、SignTool を使用してドライバーファイルをテストする方法を示しています。 この例では、*トースター*に署名を埋め込みます。これは、コマンドが実行されるディレクトリの下の*amd64*サブディレクトリにあります。 テスト証明書の名前は "contoso .com (test)" であり、"PrivateCertStore" という名前の証明書ストアにインストールされています。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.digicert.com amd64\toaster.sys
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a"></a>**エンタープライズ CA テスト証明書を使用して、テスト署名をドライバーファイルに埋め込む**

次の SignTool コマンドは、エンタープライズ CA が[ドライバーパッケージ](driver-packages.md)のテスト署名に使用するテスト証明書を発行することを前提としています。 [エンタープライズ CA テスト証明書](enterprise-ca-test-certificate.md)が証明書ストアに存在する唯一のテスト証明書である場合は、次のコマンドを使用できます。ここでは、 **/a**オプションとドライバーファイルの名前のみを指定します。 この場合、SignTool は既定でエンタープライズ CA テスト証明書を検索して使用します。

エンタープライズ CA テスト証明書に加えて他のテスト証明書を作成または取得した場合は、SignTool オプション **/s**と **/n**を使用して、テスト証明書ストアの名前とテスト証明書の名前を指定する必要があります。テスト証明書ストアにインストールされます。

```cpp
SignTool sign /v /a /t http://timestamp.digicert.com DriverFileName.sys
```

 

 





