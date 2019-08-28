---
title: 埋め込みの署名を使用したドライバーのテスト署名
description: 埋め込みの署名を使用したドライバーのテスト署名
ms.assetid: 862e89e0-f84a-4058-a32f-09ae3043b884
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcbd3e281cfce1f8bec6741c21cb0fe7097c4e52
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063928"
---
# <a name="test-signing-a-driver-through-an-embedded-signature"></a>埋め込みの署名を使用したドライバーのテスト署名


ほとんどの[ドライバーパッケージ](driver-packages.md)を正しくインストールして読み込むには、署名された[カタログファイル](catalog-files.md)が必要です。 ただし、埋め込み署名はオプションである場合もあります。 埋め込み署名とは、デジタル署名をカタログファイルに保存するのではなく、ドライバーのバイナリイメージファイル自体に追加することを意味します。 その結果、ドライバーが埋め込まれている場合、ドライバーのバイナリイメージが変更されます。

カーネルモードバイナリ (ドライバー、関連付けられている .dll ファイルなど) の埋め込み署名は、次の場合に必要です。

-   ドライバーは、ブート開始ドライバーです。 Windows Vista 以降のバージョンの windows 64 では、カーネルモードのコード署名の要件には、埋め込まれた署名が必要です。 これは、ドライバーのドライバーパッケージにデジタル署名されたカタログファイルがあるかどうかに関係なく必要です。

-   ドライバーは、カタログファイルが含まれていないドライバーパッケージを使用してインストールされます。

[カタログファイル](catalog-files.md)と同様に、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を使用して、テスト証明書を使用してカーネルモードのバイナリファイル内にデジタル署名を埋め込みます。 次のコマンドラインは、SignTool を実行して次の操作を実行する方法を示しています。

-   64ビット版の Toastpkg サンプルのバイナリファイルトースターをテストします。 WDK インストールディレクトリ内では、このファイルは*src\\general\\トースター\\toastpkg\\\\toastpkg amd64*ディレクトリにあります。

-   テスト署名には、PrivateCertStore の Contoso .com (Test) 証明書を使用します。 この証明書の作成方法の詳細については、「[テスト証明書の作成](creating-test-certificates.md)」を参照してください。

-   タイムスタンプ機関 (TSA) を使用してデジタル署名をタイムスタンプします。

*トースター*ファイルをテストするには、次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com amd64\toaster.sys
```

各項目の意味は次のとおりです。

-   **Sign**コマンドは、指定されたカタログファイル tstamd64.cat に署名するように SignTool を構成します。

-   **/V**オプションは、SignTool が成功した実行と警告メッセージを表示する詳細な操作を有効にします。

-   **/Fd**オプションは、ファイル署名の作成に使用するファイルダイジェストアルゴリズムを指定します。 既定値は SHA1 です。

-   **/S**オプションは、テスト証明書を含む証明書ストア (*PrivateCertStore)* の名前を指定します。

-   **/N**オプションは、指定された証明書ストアにインストールされている証明書 (*Contoso .com (Test))* の名前を指定します。

-   **/T**オプションは、デジタル署名のタイムスタンプ *http://timestamp.digicert.com* となる TSA () の URL を指定します。
    **重要-署名**者のコード署名の秘密キーが侵害された場合に、キーの失効に必要な情報は、タイムスタンプを含めて提供されます。  

     

-   amd64 トースターは、埋め込み署名されるカーネルモードバイナリファイルの名前を指定します *\\。*

SignTool とそのコマンドライン引数の詳細については、 [**SignTool**](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)を参照してください。

埋め込み署名を使用してドライバーをテストする方法の詳細については、「[ドライバーファイルのテスト署名](test-signing-a-driver-file.md)」を参照してください。

 

 





