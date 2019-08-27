---
title: ドライバー パッケージのカタログ ファイルのテスト署名
description: ドライバー パッケージのカタログ ファイルのテスト署名
ms.assetid: 8cc54f57-bac3-45a1-b780-48626943b446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ac1de7ec58796cfddc9daa07c199581d184c7dc
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025341"
---
# <a name="test-signing-a-driver-packages-catalog-file"></a>ドライバー パッケージのカタログ ファイルのテスト署名


[ドライバーパッケージ](driver-packages.md)の[カタログファイル](catalog-files.md)が作成または更新された後、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用してカタログファイルに署名できます。 署名した後、ドライバーパッケージのコンポーネントが変更された場合、カタログファイル内に格納されているデジタル署名は無効になります。

カタログファイルにデジタル署名すると、SignTool によって、デジタル署名がカタログファイル内に保存されます。 ドライバーパッケージのコンポーネントは、SignTool によって変更されません。 ただし、カタログファイルには、ドライバーパッケージのコンポーネントのハッシュ値が含まれているため、コンポーネントが同じ値にハッシュされる限り、カタログファイル内のデジタル署名が保持されます。

SignTool では、デジタル署名にタイムスタンプを追加することもできます。 タイムスタンプを使用すると、署名がいつ作成されたかを判断し、必要に応じてより柔軟な証明書失効オプションをサポートできます。

次のコマンドラインは、SignTool を実行して次の操作を実行する方法を示しています。

-   *Toastpkg*サンプル[ドライバーパッケージ](driver-packages.md)の*tstamd64.cat*カタログファイルにテスト署名します。 この[カタログファイル](catalog-files.md)の作成方法の詳細については、「[ドライバーパッケージのテスト署名用のカタログファイルの作成](creating-a-catalog-file-for-test-signing-a-driver-package.md)」を参照してください。

-   テスト署名には、PrivateCertStore の Contoso .com (Test) 証明書を使用します。 この証明書の作成方法の詳細については、「[テスト証明書の作成](creating-test-certificates.md)」を参照してください。

-   タイムスタンプ機関 (TSA) を使用したデジタル署名のタイムスタンプ。

*Tstamd64.cat*カタログファイルのテストに署名するには、次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com tstamd64.cat
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、指定されたカタログファイル tstamd64.cat に署名するように SignTool を構成します。

-   **/V**オプションは、SignTool が成功した実行と警告メッセージを表示する詳細な操作を有効にします。

-   **/Fd**オプションは、ファイル署名の作成に使用するファイルダイジェストアルゴリズムを指定します。 既定値は SHA1 です。

-   **/S**オプションは、テスト証明書を含む証明書ストア (*PrivateCertStore)* の名前を指定します。

-   **/N**オプションは、指定された証明書ストアにインストールされている証明書 (*Contoso .com (Test))* の名前を指定します。

-   **/T**オプションは、デジタル署名のタイムスタンプ *http://timestamp.digicert.com* となる TSA () の URL を指定します。
    **重要-署名**者のコード署名の秘密キーが侵害された場合に、キーの失効に必要な情報は、タイムスタンプを含めて提供されます。  

     

-   *tstamd64.cat*は、デジタル署名されるカタログファイルの名前を指定します。

SignTool とそのコマンドライン引数の詳細については、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を参照してください。

ドライバーパッケージのカタログファイルのテスト署名の詳細については、「[カタログファイルのテスト署名](test-signing-a-catalog-file.md)」を参照してください。

 

 





