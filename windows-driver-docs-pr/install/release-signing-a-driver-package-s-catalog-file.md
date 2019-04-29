---
title: ドライバー パッケージのカタログ ファイルのリリース署名
description: ドライバー パッケージのカタログ ファイルのリリース署名
ms.assetid: 8bfedf24-403a-406e-993d-5ab8cc790f60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1790c394107945fd7778ec1ea377ce13453aaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338631"
---
# <a name="release-signing-a-driver-packages-catalog-file"></a>ドライバー パッケージのカタログ ファイルのリリース署名


1 回、[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)が作成または更新されると、カタログでファイルを署名することも[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)します。 署名済み後、は、ドライバー パッケージのすべてのコンポーネントが変更された場合、カタログ ファイル内に格納されたデジタル署名が無効にします。

カタログ ファイルにデジタル署名すると、SignTool はカタログ ファイル内でデジタル署名を保存します。 ドライバー パッケージのコンポーネントは、SignTool によっては変更されません。 ただし、カタログ ファイルには、ドライバー パッケージのコンポーネントのハッシュ値が格納されている、ためには、カタログ ファイル内でデジタル署名は、コンポーネントが同じ値にハッシュ限り維持されます。

SignTool は、デジタル署名にタイムスタンプを追加することもできます。 タイムスタンプでは、署名の作成時に決定することができ、必要に応じてより柔軟な証明書の失効オプションをサポートします。

次のコマンドラインは、署名ツールは、次を実行する方法を示します。

-   リリース記号、 *tstamd64.cat*のカタログ ファイル、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)します。 詳細についてはこの[カタログ ファイル](catalog-files.md)が作成されるを参照してください[ドライバー パッケージのリリース署名カタログ ファイルを作成する](creating-a-catalog-file-for-release-signing-a-driver-package.md)します。

-   使用して、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)商用証明書機関 (CA) によって発行されました。

-   SPC の互換性のある複数の証明書を使用します。

-   タイム スタンプ機関 (TSA) 経由のデジタル署名にタイムスタンプを割り当てます。

リリースへの署名を*tstamd64.cat*カタログ ファイルを次のコマンドラインを実行します。

```cpp
Signtool sign /v /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドは、指定したカタログ ファイルの署名に SignTool を構成します。 *tstamd64.cat*します。

-   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

-   **/Ac**オプションは、クロス証明書を格納するファイルの名前を指定します (*MSCV VSClass3.cer*)、CA から取得します。 クロス証明書は、現在のディレクトリにない場合は、完全なパス名を使用します。

-   **/S**オプションを個人証明書ストアの名前を指定します (*MyPersonalStore)* SPC を格納しています。

-   **/N**オプションは、SPC の名前を指定します (*Contoso.com)* は指定された証明書ストアにインストールされています。

-   **/T**オプション、TSA の URL を指定します (*http://timestamp.verisign.com/scripts/timstamp.dll*) タイムスタンプをデジタル署名がこれです。
    **重要な**  キーの失効がコード署名の秘密キーの署名者の場合は、侵害の必要な情報を提供するタイムスタンプを含むです。

     

-   *tstamd64.cat*デジタル署名されるカタログ ファイルの名前を指定します。

SignTool とコマンドライン引数の詳細については、次を参照してください。 [ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)します。

ドライバー パッケージのリリース署名の詳細については、次を参照してください。[ドライバー パッケージのリリース署名](release-signing-driver-packages.md)します。

 

 





