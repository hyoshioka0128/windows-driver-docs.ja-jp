---
title: リリース署名の検証
description: リリース署名の検証
ms.assetid: 28ed3bb6-dc57-42f9-8bd5-7118619f3bf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0e13a995606f97c117aacb3a3cebb6a6486a8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339326"
---
# <a name="verifying-the-release-signature"></a>リリース署名の検証


後に、[ドライバー パッケージ](driver-packages.md)リリース署名されて、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)の署名を検証するツールを使用できます。

-   ドライバー パッケージ内の個々 のファイル。

-   ドライバーで、埋め込まれた、署名などのカーネル モード バイナリ。

このトピックの例では、Toastpkg サンプルのバイナリ ファイルの 64 ビット バージョンを使用して*toaster.sys*します。 WDK のインストール ディレクトリ内でこのファイルにある、 *src\\全般\\トースター\\toastpkg\\toastcd\\amd64*ディレクトリ。

次の例の署名を検証する*toaster.sys*で、 *tstamd64.cat*リリース署名[カタログ ファイル](catalog-files.md):

```cpp
Signtool verify /kp /v /c tstamd64.cat amd64\toaster.sys
```

各項目の意味は次のとおりです。

-   **確認**コマンドでは、指定した署名を検証する SignTool を構成します。[カタログ ファイル](catalog-files.md)(*tstamd64.cat*)。

-   **/Kp**オプションは、カーネルのポリシーが満たされていることを確認する SignTool を構成します。

-   **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

-   **/C**オプションの指定、ドライバー パッケージの[カタログ ファイル](catalog-files.md)あったリリース署名 (*tstamd64.cat*)。 埋め込まれた署名されたドライバーのデジタル署名を確認する場合は、このオプションを使用しません。

-   *amd64\\toaster.sys*を検証するファイルの名前を指定します。

「署名証明書チェーン」というラベルの付いたこのコマンドの出力、下、次の項目が true のことを確認する必要があります。

-   Microsoft コードの検証のルートと、カーネルのポリシーの証明書チェーンのルートが発行されます。

-   Microsoft コード検証ルートは、クロス証明書、クラス 3 パブリック プライマリ証明機関に発行されるが発行もします。

署名済みカタログ ファイルは、既定の Authenticode 検証ポリシーの署名も、ドライバー パッケージ内の任意のカーネル モード バイナリ ファイルで検証されます。 これにより、ファイルには、ユーザー モードのプラグ アンド プレイ インストール ダイアログ ボックスと、デバイス マネージャーを MMC スナップインのサインインが表示されます。

**注**  この例は、リリース署名の検証にのみ使用[カタログ ファイル](catalog-files.md)と埋め込まれた、署名されていないのカーネル モード バイナリ ファイル。

 

次の例は、の既定の Authenticode 検証ポリシーを確認します。 *toaster.sys*で、 *tstamd64.cat*署名済みカタログ ファイル。

```cpp
Signtool verify /pa /v /c tstamd64.cat amd64\toaster.sys
```

各項目の意味は次のとおりです。

- **確認**コマンドでは、指定したファイルに署名を検証する SignTool を構成します。<em>します。</em>

- **/Pa**オプションは、Authenticode 検証ポリシーが満たされていることを確認する SignTool を構成します。

- **/V**オプションを実行し、警告メッセージを印刷する SignTool を構成します。

- **/C**オプションの指定、ドライバー パッケージの[カタログ ファイル](catalog-files.md)でしたリリース署名 (*tstamd64.cat*)。

- *amd64\\toaster.sys*を検証するファイルの名前を指定します。

「署名証明書チェーン」というラベルの付いたこのコマンドの出力を 既定の Authenticode 証明書チェーンがして、クラス 3 パブリック プライマリ証明機関によって発行されたことを確認してください。

Windows エクスプ ローラーで、カタログ ファイル自体のデジタル署名は、次の手順に従っても確認できます。

-   右クリックし、[カタログ ファイル](catalog-files.md)選択**プロパティ**します。

-   デジタル署名されたファイルの場合、ファイルの**プロパティ** ダイアログ ボックスが追加**デジタル署名**を タブ、署名、タイムスタンプ、およびファイルの署名に使用された証明書の詳細表示されます。

ドライバー パッケージをリリース署名する方法の詳細については、次を参照してください。[ドライバー パッケージのリリース署名](release-signing-driver-packages.md)と[カタログ ファイルの署名の SPC 検証](verifying-the-spc-signature-of-a-catalog-file.md)です。

 

 





