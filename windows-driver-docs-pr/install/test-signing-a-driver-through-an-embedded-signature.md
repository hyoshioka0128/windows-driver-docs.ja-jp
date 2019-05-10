---
title: 埋め込みの署名を使用したドライバーのテスト署名
description: 埋め込みの署名を使用したドライバーのテスト署名
ms.assetid: 862e89e0-f84a-4058-a32f-09ae3043b884
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d516a8129fcd14ea0f2709506bdd1ba63f6edd2
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106366"
---
# <a name="test-signing-a-driver-through-an-embedded-signature"></a>埋め込みの署名を使用したドライバーのテスト署名


符号付き[カタログ ファイル](catalog-files.md)を正しくインストールして、ほとんどを読み込むことが必要、[ドライバー パッケージ](driver-packages.md)します。 ただし、埋め込まれた署名可能性がありますも選択肢になります。 カタログ ファイルにデジタル署名を保存せずに、ドライバーのバイナリ イメージ ファイル自体にデジタル署名を追加するには埋め込まれた署名です。 その結果、ドライバーが埋め込みで署名されたドライバーのバイナリ イメージが変更されます。

カーネル モード バイナリの埋め込まれた署名 (たとえば、ドライバーと関連付けられている .dll ファイル) に必要なときに。

-   ドライバーは、ブート開始ドライバーです。 64 ビット バージョンの Windows Vista および Windows の以降のバージョンでは、埋め込みの署名がカーネル モード コード署名の要件に必要です。 これは、ドライバーのドライバー パッケージがデジタル署名済みカタログ ファイルを持つかどうかに関係なく必要です。

-   カタログ ファイルが含まれていないドライバー パッケージをドライバーがインストールされます。

同様[カタログ ファイル](catalog-files.md)、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)テスト証明書を使用してカーネル モード バイナリ ファイル内のデジタル署名を埋め込むために使用します。 次のコマンドラインは、署名ツールは、次を実行する方法を示します。

-   テスト署名 Toastpkg サンプルの 64 ビット バージョンのバイナリ ファイル、toaster.sys します。 WDK のインストール ディレクトリ内でこのファイルにある、 *src\\全般\\トースター\\toastpkg\\toastcd\\amd64*ディレクトリ。

-   テスト署名、PrivateCertStore から Contoso.com(Test) 証明書を使用します。 この証明書の作成方法の詳細については、次を参照してください。[テスト証明書を作成する](creating-test-certificates.md)します。

-   タイムスタンプ時刻スタンプ機関 (TSA) 経由のデジタル署名。

テスト署名、 *toaster.sys*ファイルを次のコマンドラインを実行します。

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timestamp.dll amd64\toaster.sys
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドは、指定したカタログ ファイルの署名に SignTool を構成します。 tstamd64.cat します。

-   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

-   **/Fd**オプションは、ファイルの署名を作成するために使用するファイル ダイジェスト アルゴリズムを指定します。 既定値には SHA1 です。

-   **/S**オプションは、証明書ストアの名前を指定します (*PrivateCertStore)* テスト証明書を格納しています。

-   **/N**オプションは、証明書の名前を指定します (*Contoso.com(Test))* 指定された証明書ストアにインストールされています。

-   **/T**オプション、TSA の URL を指定します (*http://timestamp.verisign.com/scripts/timestamp.dll*) が、タイムスタンプ、デジタル署名します。
    **重要な**  キーの失効がコード署名の秘密キーの署名者の場合は、侵害の必要な情報を提供するタイムスタンプを含むです。

     

-   *amd64\\toaster.sys*埋め込まれた署名されるカーネル モード バイナリ ファイルの名前を指定します。

SignTool とコマンドライン引数の詳細については、次を参照してください。 [ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)します。

埋め込みの署名を使用して、ドライバーのテスト署名する方法の詳細については、次を参照してください。[テスト署名ドライバー ファイルを](test-signing-a-driver-file.md)します。

 

 





