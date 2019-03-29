---
title: プリンター詳細 Web ページをカスタマイズする
description: プリンター詳細 Web ページをカスタマイズする
ms.assetid: 4853d5de-b855-4698-9178-877455e257c5
keywords:
- カスタマイズされた印刷の Web ページ WDK、ページを作成します。
- ASP ファイル WDK プリンター
- ポート モニターを WDK の印刷、カスタマイズされた Web ページ
- カスタマイズされた Web ページ WDK、詳細ページの印刷
- 詳細ページの WDK プリンター
- Web ページ、WDK の詳細ページを印刷します。
- Web ページの WDK プリンター、詳細ページ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b22da2904aa30f44c33762c7b4db1562deb623b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580023"
---
# <a name="customizing-the-printer-details-web-page"></a>プリンター詳細 Web ページをカスタマイズする

Microsoft によって提供されるプリンターの詳細ページを置換する場合は、1 つまたは複数のカスタマイズされた ASP ファイルを指定できます。 既定のページを置換する場合、サーバーにインストールされている追加のカスタマイズされたページへのリンクと、Web で他のページへのリンクも提供できます。

Microsoft の標準場合、TCP/IP[ポート モニター](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors) (744 Tcpmon.dll) は、プリンターに使用される、カスタマイズされた ASP ファイルとプリンターの種類または製造元ごとごとに既定のプリンターの詳細ページを置換する使用できます。 カスタマイズされた ASP ファイルがインストールされていない場合は、既定のプリンターの詳細ページが使用されます。

カスタマイズされた ASP ファイルが他のポート モニター、プリンターごとの種類を使用してプリンターの既定のプリンターの詳細ページを置換することもでき、製造元ごと置換は許可されていません。

カスタマイズされた ASP ファイルをインストールするために使用されるメソッドは、カスタマイズしたファイルがプリンターの種類、製造元、またはポート モニターの既定のファイルを置き換えるかどうかを判断します。 詳細については、次を参照してください。[印刷 Web ページをカスタマイズしたインストール](installing-customized-print-web-pages.md)します。

印刷の Web ページの作成の詳細については、以下のトピックです。

[既定のプリンターの詳細ページを置き換える](replacing-the-default-printer-details-page.md)

[プリンターの詳細ページが表示されますか。](which-printer-details-page-is-displayed-.md)

[Web ページの印刷の ASP 変数](asp-variables-for-print-web-pages.md)

[Web ページの印刷の ActiveX オブジェクト](activex-objects-for-print-web-pages.md)

[Web ページの情報を更新しています](updating-web-page-information.md)
