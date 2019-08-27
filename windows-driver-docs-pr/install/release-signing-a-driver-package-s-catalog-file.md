---
title: ドライバー パッケージのカタログ ファイルのリリース署名
description: ドライバー パッケージのカタログ ファイルのリリース署名
ms.assetid: 8bfedf24-403a-406e-993d-5ab8cc790f60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410216d930a3876e61f92ed0582a1db06a317e67
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025342"
---
# <a name="release-signing-a-driver-packages-catalog-file"></a>ドライバー パッケージのカタログ ファイルのリリース署名


[ドライバーパッケージ](driver-packages.md)の[カタログファイル](catalog-files.md)が作成または更新されると、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用してカタログファイルに署名できます。 署名した後、ドライバーパッケージのコンポーネントが変更された場合、カタログファイル内に格納されているデジタル署名は無効になります。

カタログファイルにデジタル署名すると、SignTool によって、デジタル署名がカタログファイル内に保存されます。 ドライバーパッケージのコンポーネントは、SignTool によって変更されません。 ただし、カタログファイルには、ドライバーパッケージのコンポーネントのハッシュ値が含まれているため、コンポーネントが同じ値にハッシュされる限り、カタログファイル内のデジタル署名が保持されます。

SignTool では、デジタル署名にタイムスタンプを追加することもできます。 タイムスタンプを使用すると、署名がいつ作成されたかを判断し、必要に応じてより柔軟な証明書失効オプションをサポートできます。

次のコマンドラインは、SignTool を実行して次の操作を実行する方法を示しています。

-   *Toastpkg*サンプル[ドライバーパッケージ](driver-packages.md)の*tstamd64.cat*カタログファイルに署名します。 この[カタログファイル](catalog-files.md)の作成方法の詳細については、「[ドライバーパッケージのリリースに署名するためのカタログファイルの作成](creating-a-catalog-file-for-release-signing-a-driver-package.md)」を参照してください。

-   商用の証明機関 (CA) によって発行された[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)を使用します。

-   SPC に互換性のあるクロス証明書を使用します。

-   タイムスタンプ機関 (TSA) を使用してデジタル署名にタイムスタンプを割り当てます。

*Tstamd64.cat*カタログファイルに署名するには、次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.digicert.com tstamd64.cat
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、指定されたカタログファイル*tstamd64.cat*に署名するように SignTool を構成します。

-   **/V**オプションは、SignTool が成功した実行と警告メッセージを表示する詳細な操作を有効にします。

-   **/Fd**オプションは、ファイル署名の作成に使用するファイルダイジェストアルゴリズムを指定します。 既定値は SHA1 です。

-   **/Ac**オプションは、CA から取得したクロス証明書 (*MSCV-VSClass3*) を含むファイルの名前を指定します。 クロス証明書が現在のディレクトリにない場合は、完全なパス名を使用します。

-   **/S**オプションは、SPC を含む個人証明書ストア (*myのストア)* の名前を指定します。

-   **/N**オプションは、指定された証明書ストアにインストールされている SPC (*Contoso.com)* の名前を指定します。

-   **/T**オプションは、デジタル署名のタイムスタンプ *http://timestamp.digicert.com* となる TSA () の URL を指定します。
    **重要-署名**者のコード署名の秘密キーが侵害された場合に、キーの失効に必要な情報は、タイムスタンプを含めて提供されます。  

     

-   *tstamd64.cat*は、デジタル署名されるカタログファイルの名前を指定します。

SignTool とそのコマンドライン引数の詳細については、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を参照してください。

リリース署名ドライバーパッケージの詳細については、「[リリース署名ドライバーパッケージ](release-signing-driver-packages.md)」を参照してください。

 

 





