---
title: INF ファイルの記述
description: INF ファイルの記述
ms.assetid: 0A31484C-3A61-4a6d-B500-E5C69E2130F9
keywords:
- INF ファイル WDK デバイスのインストールの作成
- WDK デバイス インストールの INF ファイルの書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 983ff61588d3c7ed2f98254ba771042109e28d1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339159"
---
# <a name="writing-inf-files"></a>INF ファイルの記述


記述するとき、 [INF ファイル](inf-files.md)の[ドライバー パッケージ](driver-packages.md)、これらのガイドラインに従う必要があります。

-   INF ファイルを有効な構造を使用する必要があり、インストール プロセスの冒頭にドライバー パッケージの検証に合格するための構文を確認します。

    使用して、 [INFVerif](../devtest/infverif.md)構造と INF ファイルの構文を検証するためのツール。

-   有効な INF を含める必要があります、INF ファイル[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)と[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)セクション。 Windows Vista 以降、オペレーティング システムはコピーできませんにドライバー パッケージ、[ドライバー ストア](driver-store.md)存在し、正しく入力されていない限り、これらのセクションします。

-   ユーザー プロンプトを繰り返し表示せずに Windows で検出できるように、デバイスのインストール中に INF ファイルをコピーする必要があります。 たとえば、多機能デバイス ベースの INF ファイルは、Windows デバイスの機能の 1 つその it をインストールするたびにユーザーに確認しないでこれらの INF ファイルを検索できるように、デバイスの個々 の関数の INF ファイルをコピー可能性があります。

    INF ファイルを INF ファイルによって駆動されるインストール中を使用して、その他をステージングする場合は、Windows XP では、以降、 [ **INF CopyINF ディレクティブ**](inf-copyinf-directive.md)します。

    **注**  使用しないでください、 [ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md) INF ファイルをコピーします。

     

-   ドライバー パッケージのコンポーネントをコピーまたはシステムを直接に INF ファイルを削除する必要があります直接 *%SystemRoot%/Inf*ディレクトリ。 これは、結果、ドライバーのデジタル署名を無効にし、これにより、ドライバーが正常にロードします。

 

 





