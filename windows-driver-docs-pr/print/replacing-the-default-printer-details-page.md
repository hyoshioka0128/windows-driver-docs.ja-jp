---
title: 既定のプリンター詳細ページを置換する
description: 既定のプリンター詳細ページを置換する
ms.assetid: 451f442b-a882-4540-82dd-e96dab5e7619
keywords:
- カスタマイズされた印刷の Web ページの既定のページを置き換える WDK
- 既定のプリンターの詳細ページを置き換える
- 既定のプリンターの詳細ページ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa10d88c203be24a246eb7937bc1a0bad70308cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382575"
---
# <a name="replacing-the-default-printer-details-page"></a>既定のプリンター詳細ページを置換する





次の手順を使用して、カスタマイズされたページで、既定のプリンターの詳細ページを置き換えることができます。

1.  ページのカスタマイズされた ASP ファイルを提供します。

2.  説明されているインストール手順に従って[印刷 Web ページをカスタマイズしたインストール](installing-customized-print-web-pages.md)します。

カスタマイズされたプリンターの詳細ページには、追加のカスタマイズされたページへのリンクまたはその他のすべての Url を指定できます。 記載されている追加のカスタマイズされたページの ASP ファイルをインストールする必要があります[印刷のカスタマイズされた Web ページのインストール](installing-customized-print-web-pages.md)します。 リンクを指定する方法の詳細については、ASP のドキュメントで、Microsoft Windows SDK ドキュメントを参照してください。

印刷のカスタマイズされた Web ページには、次のテクノロジを使用できます。

[Web ページの印刷の ASP 変数](asp-variables-for-print-web-pages.md)

[Web ページの印刷の ActiveX オブジェクト](activex-objects-for-print-web-pages.md)

カスタマイズされた COM オブジェクト

作成して、COM オブジェクトを使用する方法については、Windows SDK のドキュメントを参照してください。

**注**   ASP ファイルを使用して作成されたすべての印刷 Web ページは、1 つの ASP アプリケーションから生成されます。
システム ディスクのプリンターのサブディレクトリに含まれている、Globals.asp という名前のファイルを変更する必要があります。

Microsoft は、予告なく印刷、Web ページを変更する権利を留保します。 そのため、カスタマイズされた ASP ファイルでは、Microsoft 提供の ASP ファイルの内容に依存する必要があります。

 

 

 




