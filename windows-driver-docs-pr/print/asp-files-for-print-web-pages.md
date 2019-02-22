---
title: Web ページの印刷の ASP ファイル
description: Web ページの印刷の ASP ファイル
ms.assetid: 01ca39ed-be16-41fb-b432-1cbd0908358d
keywords:
- カスタマイズされた印刷 Web ページ WDK、ASP ファイル
- ASP ファイル WDK プリンター
- WDK 印刷の Web ページ、ASP ファイル
- Web ページの WDK プリンター、ASP ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 842227883a534b96507975e210f077872a904ec2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532589"
---
# <a name="asp-files-for-print-web-pages"></a>Web ページの印刷の ASP ファイル





印刷の Web ページを作成するには、ASP ファイルを使用します。 マイクロソフトでは、以下を作成する ASP ファイルが Web ページを印刷を提供します。

- URL http:// によって参照されているプリント サーバー ページ<em>&lt;ServerName&gt;</em>/printers、場所*&lt;ServerName&gt;* DNS または WINS を表しますプリント サーバーの名前。 このページには、サーバーにインストールされているすべてのプリンターのページへのリンクが含まれています。

- 各サーバーの印刷キューの印刷キュー ページです。 これらのページには、プリント サーバー ページで、リンクからアクセスまたは URL http:// を使用して、ブラウザーから直接参照できる<em>&lt;ServerName&gt;</em>  /  *&lt;ShareName&gt;* します。

- キュー内にドキュメント、プリンターのプロパティ、およびプリンター固有の詳細の追加のページ。 印刷キューのページのフレーム内では、これらのページが表示されます。

プリンター固有の詳細ページは、その ASP ファイルを置き換えることでカスタマイズできます。 詳細については、次を参照してください。[プリンターの詳細の Web ページをカスタマイズする](customizing-the-printer-details-web-page.md)します。

 

 




