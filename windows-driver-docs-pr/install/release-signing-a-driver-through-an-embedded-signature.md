---
title: 埋め込みの署名を使用したドライバーのリリース署名
description: 埋め込みの署名を使用したドライバーのリリース署名
ms.assetid: ffea2479-83ee-4d94-a5e6-73ecea9fc17d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b118cb143182722d0f65afefe8ba9bf132a0c7d
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025338"
---
# <a name="release-signing-a-driver-through-an-embedded-signature"></a>埋め込みの署名を使用したドライバーのリリース署名


ほとんどの[ドライバーパッケージ](driver-packages.md)を正しくインストールして読み込むには、署名された[カタログファイル](catalog-files.md)が必要です。 ただし、埋め込み署名はオプションである場合もあります。 埋め込み署名とは、デジタル署名をカタログファイルに保存するのではなく、ドライバーのバイナリイメージファイル自体に追加することを意味します。 その結果、ドライバーが埋め込まれている場合、ドライバーのバイナリイメージが変更されます。

カーネルモードバイナリ (ドライバー、関連付けられている .dll ファイルなど) の埋め込み署名は、次の場合に必要です。

-   ドライバーは、*ブート開始ドライバー*です。 Windows Vista 以降のバージョンの windows 64 では、[カーネルモードのコード署名の要件](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)は、*ブート開始ドライバー*に埋め込まれた署名が必要であることを前提としています。 これは、ドライバーのドライバーパッケージにデジタル署名されたカタログファイルがあるかどうかに関係なく必要です。

-   ドライバーは、カタログファイルが含まれていないドライバーパッケージを使用してインストールされます。

[カタログファイル](catalog-files.md)と同様に、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)ツールを使用して、テスト証明書を使用してカーネルモードのバイナリファイル内にデジタル署名を埋め込みます。 次のコマンドラインは、SignTool を実行して次の操作を実行する方法を示しています。

-   64ビット版の Toastpkg サンプルのバイナリファイルトースターをテストします。 WDK インストールディレクトリ内では、このファイルは*src\\general\\トースター\\toastpkg\\\\toastpkg amd64*ディレクトリにあります。

-   商用の証明機関 (CA) によって発行された[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)を使用します。

-   SPC に互換性のあるクロス証明書を使用します。

-   タイムスタンプ機関 (TSA) を使用してデジタル署名にタイムスタンプを割り当てます。

*トースター*ファイルをテストするには、次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.digicert.com amd64\toaster.sys
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、指定されたカーネルモードのバイナリファイル*amd64\\トースター*に署名するように SignTool を構成します。

-   **/V**オプションは、SignTool が成功した実行と警告メッセージを表示する詳細な操作を有効にします。

-   **/Fd**オプションは、ファイル署名の作成に使用するファイルダイジェストアルゴリズムを指定します。 既定値は SHA1 です。

-   **/Ac**オプションは、CA から取得したクロス証明書 (*MSCV-VSClass3*) を含むファイルの名前を指定します。 クロス証明書が現在のディレクトリにない場合は、完全なパス名を使用します。

-   **/S**オプションは、SPC を含む個人証明書ストア (*myのストア)* の名前を指定します。

-   **/N**オプションは、指定された証明書ストアにインストールされている証明書 (*Contoso.com)* の名前を指定します。

-   **/T**オプションは、デジタル署名のタイムスタンプ *http://timestamp.digicert.com* となる TSA () の URL を指定します。

    **重要-署名**者のコード署名の秘密キーが侵害された場合に、キーの失効に必要な情報は、タイムスタンプを含めて提供されます。  

     

-   amd64 トースターは、埋め込み署名されるカーネルモードバイナリファイルの名前を指定します *\\。*

SignTool とそのコマンドライン引数の詳細については、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を参照してください。

埋め込み署名を使用したドライバーのリリースの詳細については、「ドライバー[パッケージのリリース](release-signing-driver-packages.md)と[ドライバーファイルのリリース](release-signing-a-driver-file.md)署名」を参照してください。

 

 





