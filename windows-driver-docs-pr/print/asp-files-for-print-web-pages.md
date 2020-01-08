---
title: 印刷 Web ページの ASP ファイル
description: 印刷 Web ページの ASP ファイル
ms.assetid: 01ca39ed-be16-41fb-b432-1cbd0908358d
keywords:
- カスタマイズされた印刷 Web ページ WDK、ASP ファイル
- ASP ファイル WDK プリンター
- Web ページ WDK、ASP ファイルを印刷する
- Web ページ WDK プリンター、ASP ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d2cde131c51750450536684a7af752de72ec04
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652932"
---
# <a name="asp-files-for-print-web-pages"></a>印刷 Web ページの ASP ファイル





印刷 Web ページは、ASP ファイルを使用して作成されます。 Microsoft では、次の印刷 Web ページを作成する ASP ファイルを提供しています。

- URL によって参照されているプリントサーバーページ https://<em>&lt;servername&gt;</em>/printers。ここで *&lt;servername&gt;* はプリントサーバーの DNS または WINS 名を表します。 このページには、サーバーにインストールされているすべてのプリンターのページへのリンクが表示されます。

- 各サーバーの印刷キューの印刷キューページ。 これらのページには、[プリントサーバー] ページのリンクからアクセスできます。または、URL https://<em>&lt;ServerName&gt;</em>/ *&lt;ShareName&gt;* を使用してブラウザーから直接参照することもできます。

- キューに登録されたドキュメントの追加ページ、プリンターのプロパティ、およびプリンター固有の詳細。 これらのページは、[印刷キュー] ページのフレーム内に表示されます。

プリンター固有の詳細ページは、ASP ファイルを置き換えることでカスタマイズできます。 詳細については、「[プリンターの詳細のカスタマイズ」 Web ページ](customizing-the-printer-details-web-page.md)を参照してください。

 

 




