---
title: 印刷 Web ページを表示する
description: 印刷 Web ページを表示する
ms.assetid: c2cf782c-0f53-47e1-8c5e-1e2aa87613c4
keywords:
- インターネット WDK の印刷、印刷の Web ページを表示します。
- 印刷の Web ページを表示します。
- 印刷の Web ページの表示
- 印刷の Web ページ WDK, 表示
- Web ページの WDK プリンター, 表示
- プリント サーバー ページ WDK
- プリント サーバーのページを表示します。
- Url の WDK を印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 706b189efd5834df0f3246d32407ff65de6b8292
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345287"
---
# <a name="viewing-print-web-pages"></a>印刷 Web ページを表示する





任意の種類のクライアント プラットフォームで実行されているすべてのインターネット ブラウザーでは、ユーザーは、Microsoft Windows 2000 の状態を表示または後でサーバーと、接続されているプリンターを印刷する Web ページを表示できます。 Microsoft では、これらの Web ページを生成するサーバーに常駐 HTML ファイルのセットを提供します。 Url を使用して、クライアント ブラウザーによっては、プリント サーバーと各サーバーにインストールされたプリンター web ページを参照できます。 これらのページからのリンクで追加のページを参照できます。

Web ページをサポートするために Windows 2000 プリント サーバーは Microsoft インターネット インフォメーション サーバー (IIS) または Microsoft ピアの Web サーバーで Windows 2000 Professional ソフトウェアでいずれかの Windows 2000 Server ソフトウェアが実行する必要があります。

Web ページをサポートするために Windows XP プリント サーバーは Microsoft インターネット インフォメーション サーバー (IIS) または Microsoft ピアの Web サーバーで Windows XP Professional ソフトウェアでいずれかの Microsoft Windows Server 2003 のソフトウェアが実行する必要があります。 Windows XP Home Edition でプリント サーバーが Web ページをサポートしていないことに注意してください。

プリント サーバーのページを表示するには、ユーザーは、次の URL 形式を指定します。

http://&lt;ServerName&gt;/printers

場所&lt;ServerName&gt; (インターネット接続用の DNS 名) またはイントラネット接続用の WINS 名のいずれかのサーバー名です。 URL は、プリント サーバーのページを生成する HTML ファイルを指します。

サーバーのページでは、サーバーで使用可能な各印刷キューの印刷キューのページへのリンクを提供します。 印刷キューの共有は、すべてのユーザーがアクセスできます。 ユーザーは、次の形式で URL を指定して共有プリンターの印刷キューのページを参照もできます。

http://&lt;ServerName&gt;/&lt;ShareName&gt;

場所&lt;ShareName&gt;は、プロパティ シートで指定されている、印刷キューの共有の名前です。

ユーザーは、印刷のフォルダー内のプリンターのリンクを選択する場合は、Windows Internet Explorer が自動的に開始し、印刷キューのページの URL にアクセスします。 または、既に説明したとおり、ユーザーことができますプリント サーバー ページまたはページを表示、印刷キュー、HTML ブラウザーにページの URL を指定することで。

印刷の Web ページは、Microsoft Active Server Pages (ASP) によって、解釈されるテンプレート ファイルから生成されます。 これらのテンプレート (ASP ファイルと呼ばれます) を含む標準の HTML タグと ASP スクリプト タグ (&lt;% と %&gt;)。

Active Server Pages インタープリターには、ASP スクリプト タグ内のテキストが検出されると、テキストを処理する適切なスクリプト言語インタープリター (JScript VBScript など) を呼び出します。 結果の HTML データ ストリームは、クライアント ブラウザーに送信されます。

Microsoft Active Server Pages の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

一連の COM ベース[Web ページの印刷の ActiveX オブジェクト](activex-objects-for-print-web-pages.md)プリンターのプロパティと SNMP 情報の取得の (Oleprn.dll) で提供される、関連付けられたオートメーション インターフェイスを使用します。

ユーザーが特定のサーバーやプリンターの Web ページを表示したい場合に、次の手順が行われます。

1.  ユーザーは、適切な URL を指定する、ブラウザーを採用しています。 URL は、指定したプリント サーバー上のテンプレート ファイルのいずれかを指します。

2.  IIS の一部では、サーバーに常駐 Active Server Pages インタープリターは、ASP スクリプト タグを検索、スクリプトのテキストを解釈する適切なスクリプト言語インタープリターを起動し、返される結果を HTML のデータ ストリームに配置します。

3.  サーバーで、ASP インタープリターでは、クライアントのブラウザーに、結果の HTML ストリームを送信します。

次の図は、プロセスでは、クライアントからプリンター URL を送信するプリント サーバー、およびその関連付けられている HTML ストリームをクライアントに返される方法を示します。

![印刷の url をクライアントからプリント サーバーに送信するかを示す図](images/prnturl.png)

 

 




