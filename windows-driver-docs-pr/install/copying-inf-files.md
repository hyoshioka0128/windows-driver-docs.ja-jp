---
title: INF ファイルのコピー
description: INF ファイルのコピー
ms.assetid: 3ef92943-6462-4fe7-bd9b-8235083e8e16
keywords:
- INF ファイル、WDK デバイス インストールのコピー
- INF ファイルのコピー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c64e22b166a4da7de7cd6dc969da2862725be3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344302"
---
# <a name="copying-inf-files"></a>INF ファイルのコピー





ユーザー プロンプトを繰り返し表示せずに Windows で検出できるように、デバイスのインストール中に INF ファイルをコピーする必要があります。 たとえば、多機能デバイス ベースの INF ファイルは、Windows デバイスの機能の 1 つをインストールするごとにユーザーに確認しないでこれらの INF ファイルを検索できるように、デバイスの個々 の関数の INF ファイルをコピー可能性があります。

INF ファイルをコピーする、INF ファイルを使用できる、 [ **INF CopyINF ディレクティブ**](inf-copyinf-directive.md)します。

これにより。

-   INF ファイルと共に、ユーザーが存在する場合は、適切なカタログ ファイルをインストールします。

-   INF ファイルを上書きしませんし、その他の INF ファイルは上書きされませんように一意の名前を INF ファイルに付けます。

-   デバイスのファイルのコピー元のソース メディアのパスを保持します。

-   Windows の将来のバージョンとの互換性を確認します。

インストール ソフトウェア システムを直接に INF ファイルをコピーしない必要があります *%SystemRoot%/inf*ディレクトリ。 このセクションでは説明しません手法を使用して INF ファイルをコピーすると、ドライバーのデジタル署名が無効になります。

 

 





