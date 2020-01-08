---
title: 印刷 Web ページを表示する
description: 印刷 Web ページを表示する
ms.assetid: c2cf782c-0f53-47e1-8c5e-1e2aa87613c4
keywords:
- インターネット印刷 WDK, 印刷 Web ページの表示
- 印刷 Web ページの表示
- 印刷 Web ページの表示
- Web ページ WDK の印刷、表示
- Web ページの WDK プリンター、表示
- プリントサーバーページ WDK
- プリントサーバーページの表示
- Url の印刷 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 489bf59109547b89cc3c12118dc55d12202ca6e9
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653014"
---
# <a name="viewing-print-web-pages"></a>印刷 Web ページを表示する





任意の種類のクライアントプラットフォームで実行されている任意のインターネットブラウザーを使用すると、Microsoft Windows 2000 以降のプリントサーバーと接続されているプリンターの状態を表示する Web ページを表示できます。 Microsoft では、これらの Web ページを生成する一連のサーバー常駐 HTML ファイルを提供しています。 プリントサーバーおよびサーバーにインストールされた各プリンターの Web ページは、Url を使用してクライアントブラウザーから参照できます。 追加のページは、これらのページのリンクから参照できます。

Windows 2000 プリントサーバーで Web ページをサポートするには、Microsoft インターネットインフォメーションサービス (IIS) を使用した Windows 2000 サーバーソフトウェア、または Microsoft ピア Web サーバーを使用した Windows 2000 Professional ソフトウェアのいずれかを実行している必要があります。

Windows XP プリントサーバーで Web ページをサポートするには、microsoft インターネットインフォメーションサービス (IIS) を使用した Microsoft Windows Server 2003 ソフトウェアか、Microsoft ピア Web サーバーを使用した Windows XP Professional ソフトウェアを実行している必要があります。 Windows XP Home Edition のプリントサーバーでは、Web ページがサポートされていないことに注意してください。

プリントサーバーページを表示するには、次の URL 形式を指定します。

https://&lt;ServerName&gt;/printers

ここで &lt;ServerName&gt; はサーバー名 (インターネット接続の場合は DNS 名、イントラネット接続の場合は WINS 名) です。 URL は、プリントサーバーのページを生成する HTML ファイルを指しています。

[サーバー] ページには、サーバーで使用可能な各印刷キューの [印刷キュー] ページへのリンクが表示されます。 共有印刷キューには、すべてのユーザーがアクセスできます。 ユーザーは、次の形式の URL を指定することで、共有プリンターの印刷キューページを参照することもできます。

https://&lt;ServerName&gt;/&lt;ShareName&gt;

ここで &lt;ShareName&gt; は、プロパティシートで指定されている印刷キューの共有名です。

ユーザーが印刷フォルダー内のプリンターのリンクを選択すると、Windows Internet Explorer が自動的に起動し、印刷キューページの URL にアクセスします。 または、既に説明したように、ユーザーは、任意の HTML ブラウザーへのページの URL を指定することによって、プリントサーバーページまたは印刷キューページを表示できます。

印刷 Web ページは、Microsoft Active Server Pages (ASP) で解釈できるテンプレートファイルから生成されます。 これらのテンプレート (ASP ファイルと呼ばれます) には、標準の HTML タグと ASP スクリプトタグ (&lt;% および%&gt;) が含まれています。

Active Server ページインタープリターが ASP スクリプトタグ内のテキストを検出すると、適切なスクリプト言語インタープリター (JScript や VBScript など) を呼び出してテキストを処理します。 その後、結果の HTML データストリームがクライアントブラウザーに送信されます。

Microsoft Active Server ページの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

[印刷 Web ページ](activex-objects-for-print-web-pages.md)の一連の COM ベースの ActiveX オブジェクトは、関連付けられたオートメーションインターフェイスを使用して、プリンターのプロパティと SNMP 情報を取得するために (oleprn .dll に) 提供されます。

ユーザーが特定のサーバーまたはプリンターの Web ページを表示したい場合は、次の手順が実行されます。

1.  ユーザーは、ブラウザーを採用して適切な URL を指定します。 URL は、指定されたプリントサーバー上のいずれかのテンプレートファイルを指しています。

2.  IIS の一部であるサーバー常駐 Active Server ページインタープリターは、ASP スクリプトタグを検索し、適切なスクリプト言語インタープリターを呼び出してスクリプトテキストを解釈し、返された結果を HTML データストリームに配置します。

3.  サーバー上の ASP インタープリターは、生成された HTML ストリームをクライアントのブラウザーに送信します。

次の図は、プリンターの URL がクライアントからプリントサーバーに送信されるプロセスと、関連付けられている HTML ストリームがクライアントに返される方法を示しています。

![クライアントからプリントサーバーへの印刷 url の送信を示す図](images/prnturl.png)

 

 




