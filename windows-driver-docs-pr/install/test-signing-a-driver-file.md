---
title: テスト署名ドライバー ファイル
description: テスト署名ドライバー ファイル
ms.assetid: 3d73d632-e910-43e7-a8fd-c78a11df0206
keywords:
- テスト署名ドライバー パッケージにドライバー ファイル
- テスト署名を埋め込み、WDK のドライバー パッケージの署名
- WDK のドライバー ファイルの埋め込み署名
- 埋め込まれた、WDK の署名
- デジタル署名 WDK、埋め込まれました。
- テスト証明書の MakeCert WDK
- テスト署名ドライバー ファイル WDK
- 市販のテスト証明書 WDK
- エンタープライズ CA テスト証明書 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7442f05d8d409f950b4e364fae179a61ce2e1b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557935"
---
# <a name="test-signing-a-driver-file"></a>テスト署名ドライバー ファイル


使用[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)次のトピックの説明に従って、ドライバー ファイルに署名を埋め込むには。

[MakeCert テスト証明書または市販のテスト証明書を使用して、ドライバー ファイルにテスト署名を埋め込むには](#using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-)

[エンタープライズ CA のテスト証明書を使用して、ドライバー ファイルにテスト署名を埋め込むには](#using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a)

### <a href="" id="using-a-makecert-test-certificate-or-a-commercial-test-certificate-to-"></a> MakeCert テスト証明書または市販のテスト証明書を使用して、ドライバー ファイルにテスト署名を埋め込むには

使用して、ドライバー ファイルに署名を埋め込むには次の SignTool コマンドを使用して、 [MakeCert テスト証明書](makecert-test-certificate.md)または[市販のテスト証明書](commercial-test-certificate.md)します。

```cpp
SignTool sign /v /s TestCertStoreName /n TestCertName /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

各項目の意味は次のとおりです。

-   Sign コマンドでは、SignTool DriverFileName.sys ドライバー ファイルに署名を埋め込むには構成します。

-   **/V** /verbose オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/S** *TestCertStoreName*オプションという名前のテスト証明書を含むテスト証明書ストアの名前を提供する*TestCertName*します。

-   **/N** *TestCertName*オプションという名前の証明書ストアにインストールされているテスト証明書の名前を提供する*TestCertStoreName*します。 テスト証明書には、MakeCert テスト証明書または市販のテスト証明書のいずれかを指定できます。

-   **/T**  * http://timestamp.verisign.com/scripts/timstamp.dll *オプションは、VeriSign を提供するパブリックに利用可能なタイム スタンプ サーバーの URL を提供します。

-   *DriverFileName.sys*ドライバー ファイルの名前を指定します。

次のコマンドは、テスト署名ドライバー ファイルを SignTool を使用する方法を示します。 この例での署名を埋め込みます*Toaster.sys*、これは、 *amd64*コマンドが実行されるディレクトリのサブディレクトリ。 テスト証明書の名前は"contoso.com(test)"と"PrivateCertStore"という名前の証明書ストアにインストールされます。

```cpp
SignTool sign /v /s PrivateCertStore /n contoso.com(test) /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

### <a href="" id="using-an-enterprise-ca-test-certificate-to-embed-a-test-signature-in-a"></a>**エンタープライズ CA のテスト証明書を使用して、ドライバー ファイルにテスト署名を埋め込むには**

次の SignTool コマンドでは、エンタープライズ CA が、テストへの署名を使用したテスト証明書を発行する前提としています、[ドライバー パッケージ](driver-packages.md)します。 場合、[テスト証明書をエンタープライズ CA](enterprise-ca-test-certificate.md) 、証明書ストアに存在する唯一のテスト証明書は、次のコマンドを使用できますのみ指定する、 **/a**オプションとの名前、ドライバー ファイルです。 このような状況では、SignTool は検索し、既定では、エンタープライズ CA テスト証明書を使用します。

エンタープライズ CA のテスト証明書だけでなく他のテスト証明書を取得または作成した場合は、SignTool オプションを使用する必要があります **/s**と **/n**テスト証明書ストアの名前を指定してテスト証明書ストアにインストールされているテスト証明書の名前。

```cpp
SignTool sign /v /a /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

 

 





