---
title: MakeCat を使用して、カタログ ファイルを作成するには
description: MakeCat を使用して、カタログ ファイルを作成するには
ms.assetid: c9f9360b-2b1d-4060-af4d-8d281319e181
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae642f6045a968a8f990fe5acec10add2609f7d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538446"
---
# <a name="using-makecat-to-create-a-catalog-file"></a>MakeCat を使用して、カタログ ファイルを作成するには


使用することができます、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)を作成するツール、[カタログ ファイル](catalog-files.md)の[ドライバー パッケージ](driver-packages.md)します。

INF ファイルを使用してインストールされていないドライバー パッケージのカタログ ファイルの作成にのみ、MakeCat ツールを使用する必要があります。 INF ファイルを使用して、ドライバー パッケージをインストールする場合は、使用、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)カタログ ファイルを作成するためのツール。 Inf2Cat には、パッケージの INF ファイル内で参照される、ドライバー パッケージ内のすべてのファイルに自動的に含まれています。 Inf2Cat ツールを使用する方法の詳細については、[カタログ ファイルを作成するのを使用して Inf2Cat](using-inf2cat-to-create-a-catalog-file.md)を参照してください。

**注**  を作成し、カタログ ファイルへの署名、代わりに埋め込むことも、署名のカーネル モード バイナリの[ドライバー パッケージ](driver-packages.md)、ドライバー パッケージを提供するすべての .dll ファイルなどです。 この手順の詳細については、[テスト署名ドライバーは、埋め込みの署名](test-signing-a-driver-through-an-embedded-signature.md)を参照してください。

 

カタログ ファイルを作成する必要がありますまず手動で作成するカタログの定義ファイル (*.cdf*) カタログ ヘッダー属性やファイルのエントリを説明します。 このファイルが作成されると、行うことができますし、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)カタログ ファイルを作成するためのツール。 MakeCat ツールでは、次の処理時に、 *.cdf*ファイル。

-   各ファイルに記載されている属性の一覧を確認、 *.cdf*ファイル。

-   表示されている属性を追加します、[カタログ ファイル](catalog-files.md)します。

-   、暗号化ハッシュを生成または*拇印*、リスト内のファイルのそれぞれの。

-   カタログ ファイルでは、各ファイルの拇印を格納します。

このトピックでは、作成する方法を説明します、 *.cdf*の 64 ビットのカーネル モード バイナリ ファイルのファイル、 *ToastPkg*サンプル ドライバー パッケージ。 WDK のインストール ディレクトリ内でこれらのバイナリ ファイル内にある、 *src\\全般\\トースター\\toastpkg\\toastcd\\amd64*ディレクトリ。

作成する、 *.cdf*ファイルを*ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)次の操作を行います。

1.  メモ帳を起動し、次の例からテキストをコピーします。 その属性と共に、カタログ化するファイルの一覧が含まれています。

    ```cpp
    [CatalogHeader]
    Name=tstamd64.cat
    PublicVersion=0x0000001
    EncodingType=0x00010001
    CATATTR1=0x10010001:OSAttr:2:6.0
    [CatalogFiles]
    <hash>File1=amd64\toaster.pdb
    <hash>File2=amd64\toaster.sys
    <hash>File3=amd64\toastva.exe
    <hash>File4=amd64\toastva.pdb
    <hash>File5=amd64\tostrcls.dll
    <hash>File6=amd64\tostrcls.pdb
    <hash>File7=amd64\tostrco2.dll
    <hash>File8=amd64\tostrco2.pdb
    ```

2.  ファイルに保存します*tstamd64.cdf*ドライバー パッケージと同じフォルダーにします。
    **注**  を複数のプラットフォーム用のドライバーを構築する場合は、プラットフォームごとに別々 のカタログ ファイルを作成します。

     

次のコマンド ラインでカタログ ファイルを作成する方法を示しています、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)ツールを使用して、 *tstamd64.cdf*ファイル。

```cpp
makecat -v tstamd64.cdf
```

という名前のファイル、ツールを実行した後*tstamd64.cat*が作成されます。

MakeCat ツールとコマンドライン引数の詳細については、次を参照してください。、[を使用して MakeCat](https://go.microsoft.com/fwlink/p/?linkid=70086) web サイト。

MakeCat ツールを使用する方法の詳細については、[非 PnP ドライバー パッケージのカタログ ファイルを作成する](creating-a-catalog-file-for-a-non-pnp-driver-package.md)を参照してください。

 

 





