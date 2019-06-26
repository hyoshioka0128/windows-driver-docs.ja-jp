---
title: ドライバー パッケージのカタログ ファイルのテスト署名
description: ドライバー パッケージのカタログ ファイルのテスト署名
ms.assetid: 8cc54f57-bac3-45a1-b780-48626943b446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ff416c6bdd9a774846d0166876ab723457e8a7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380994"
---
# <a name="test-signing-a-driver-packages-catalog-file"></a>ドライバー パッケージのカタログ ファイルのテスト署名


後に、[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)が作成または更新されると、カタログでファイルを署名することも[ **SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)。 署名済み後、は、ドライバー パッケージのすべてのコンポーネントが変更された場合、カタログ ファイル内に格納されたデジタル署名が無効にします。

カタログ ファイルにデジタル署名すると、SignTool はカタログ ファイル内でデジタル署名を保存します。 ドライバー パッケージのコンポーネントは、SignTool によっては変更されません。 ただし、カタログ ファイルには、ドライバー パッケージのコンポーネントのハッシュ値が格納されている、ためには、カタログ ファイル内でデジタル署名は、コンポーネントが同じ値にハッシュ限り維持されます。

SignTool は、デジタル署名にタイムスタンプを追加することもできます。 タイムスタンプ署名の作成時に決定することができ、必要な場合より柔軟な証明書の失効オプションをサポートしています。

次のコマンドラインは、署名ツールは、次を実行する方法を示します。

-   テスト署名、 *tstamd64.cat*のカタログ ファイル、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)します。 詳細についてはこの[カタログ ファイル](catalog-files.md)が作成されるを参照してください[ドライバー パッケージのテスト署名カタログ ファイルを作成する](creating-a-catalog-file-for-test-signing-a-driver-package.md)します。

-   テスト署名、PrivateCertStore から Contoso.com(Test) 証明書を使用します。 この証明書の作成方法の詳細については、次を参照してください。[テスト証明書を作成する](creating-test-certificates.md)します。

-   タイム スタンプ機関 (TSA) 経由のデジタル署名のタイムスタンプ。

テスト署名、 *tstamd64.cat*カタログ ファイルを次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドは、指定したカタログ ファイルの署名に SignTool を構成します。 tstamd64.cat します。

-   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

-   **/Fd**オプションは、ファイルの署名を作成するために使用するファイル ダイジェスト アルゴリズムを指定します。 既定値には SHA1 です。

-   **/S**オプションは、証明書ストアの名前を指定します (*PrivateCertStore)* テスト証明書を格納しています。

-   **/N**オプションは、証明書の名前を指定します (*Contoso.com(Test))* 指定された証明書ストアにインストールされています。

-   **/T**オプション、TSA の URL を指定します ( *http://timestamp.verisign.com/scripts/timstamp.dll* ) が、タイムスタンプ、デジタル署名します。
    **重要な**  キーの失効がコード署名の秘密キーの署名者の場合は、侵害の必要な情報を提供するタイムスタンプを含むです。

     

-   *tstamd64.cat*デジタル署名されるカタログ ファイルの名前を指定します。

SignTool とコマンドライン引数の詳細については、次を参照してください。 [ **SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)します。

テスト署名の詳細については、ドライバー パッケージのカタログ ファイルを参照してください[カタログ ファイルのテスト署名](test-signing-a-catalog-file.md)します。

 

 





