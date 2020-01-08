---
title: アプリケーションから URL に印刷する
description: アプリケーションから URL に印刷する
ms.assetid: bc9aedb4-1d64-4b70-b14b-1392f914a635
keywords:
- インターネット印刷 WDK、Url への出力
- URL-識別された印刷キュー WDK
- フレンドリ名 WDK プリンター
- Url への印刷 WDK
- Web ページ WDK を印刷し、Url に印刷する
- Web ページの WDK プリンター、Url への出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a1aa24908c83620506a68c4f779c4e768deb6c
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653000"
---
# <a name="printing-to-urls-from-applications"></a>アプリケーションから URL に印刷する





アプリケーションの観点からは、URL で識別される印刷キューへの印刷は、UNC で識別される印刷キューへの出力と同じです。 通常、アプリケーションは、URL を使って印刷キューにアクセスすることを認識しません。

[印刷 Web ページを表示](viewing-print-web-pages.md)することで、ユーザーは URL で識別された印刷キューをインストールして接続できます。 この場合、印刷キューには、プリントサーバー上にあるのと同じ "表示名" が割り当てられます。この表示名は、ユーザーの [印刷] フォルダーに一覧表示されます。

一般に、アプリケーションは、UNC で識別される印刷キューの場合と同様に、印刷キューをフレンドリ名で参照します。 ローカル印刷プロバイダー (たとえば、GDI 呼び出しを行うアプリケーションによって発生する) の**OpenPrinter**関数の呼び出しには、フレンドリ名が含まれます。 さらに、ローカル印刷プロバイダーは、印刷キューの URL を指定して、HTTP 印刷プロバイダー (Inetpp .dll) で**OpenPrinter**を呼び出します。

印刷キューをフレンドリ名で参照するアプリケーションは、通常、印刷キューがローカルとネットワークのどちらであるか、またはネットワークプロトコルが RPC、SMB、HTTP のいずれであるかを認識しません。 ただし、アプリケーションは必要に応じて、URL を指定して直接**OpenPrinter**を呼び出すことができます。 **OpenPrinter**の url を指定する場合は、次の url 形式を使用する必要があります。

https://&lt;ServerName&gt;/プリンター/&lt;ShareName&gt;/.printer

&lt;ServerName&gt; はサーバー名 (インターネット接続の場合は DNS 名、イントラネット接続の場合は WINS 名)、"printers" はサーバー上の仮想ディレクトリ、&lt;ShareName&gt; はプロパティシートで指定されている印刷キューの共有名です。 (仮想ディレクトリについては Microsoft Windows SDK のドキュメントを参照してください)。

クライアントのスプーラコンポーネントまたはアプリケーションが**OpenPrinter**を呼び出し、URL を指定すると、その後のスプーラ機能 ( **startdocprinter**、 **writeprinter**など) への呼び出しは、クライアントの HTTP 印刷プロバイダーによって処理されます。 HTTP 印刷プロバイダーは、URL に引数を追加し、結果の URL 文字列をプリントサーバーに送信します。

Microsoft Windows 2000 プリントサーバーで Url を含む印刷要求を受け入れるには、次のいずれかを実行している必要があります。

-   Microsoft Internet Information Server (IIS) を使用した Windows 2000 サーバーソフトウェア、または

-   Microsoft ピア Web サーバーを使用した Windows 2000 Professional ソフトウェア

Windows XP プリントサーバーで Url を含む印刷要求を受け入れるには、次のいずれかを実行している必要があります。

-   Microsoft インターネットインフォメーションサービス (IIS) を使用した microsoft Windows Server 2003 ソフトウェア

-   Microsoft ピア Web サーバーを使用した Windows XP Professional ソフトウェア

Windows XP Home Edition プリントサーバーでは、Url を含む要求を受け付けることはできませ**ん  。**

 

プリントサーバーでは、IIS またはピア Web サーバーは URL 文字列を受け取ります。 クライアントシステムの Inetpp によって文字列に追加される引数により、サーバーは Msw3prt に含まれている HTTP プリントサーバーを呼び出します。 HTTP プリントサーバーは、生の形式のプリンターデータを受け入れ、それをローカルの印刷スプーラに送信します。

プリンターデータはインターネット印刷プロトコル (IPP 1.0) を使用してクライアントからサーバーに送信されます。これは、インターネット技術標準化委員会 (IETF) の Printer Working Group (PWG) によって定義されます。

次の図は、クライアントが URL で識別される印刷キューに出力する場合に、クライアントアプリケーションからプリントサーバーのスプーラへの印刷データのパスを示しています。

![url で識別された印刷キューへの印刷を示す図](images/prntpath.png)

図に示すように、クライアントとサーバーの両方が Windows 2000 以降のシステムである場合は、クライアントとサーバー間の通信には通常、RPC プロトコルが使用されます (常にではありません)。 (詳細については、「 [Web ページから印刷ドライバーをインストールする](installing-print-drivers-from-a-web-page.md)」を参照してください)。クライアントとサーバーの両方が Windows 2000 以降のシステムではない場合は、HTTP が使用されます。 HTTP は、内部ネットワークカードを搭載し、IPP 1.0 をサポートするプリンターにも使用されます。そのため、サーバーに接続されません。

プリントサーバーのセキュリティは、プリントサーバー上で実行される IIS によって提供されます。 IIS でサポートされるセキュリティメカニズムについては、「 *Iis リソースガイド*」で説明されています。これは * * に含まれています。

*Microsoft Windows 2000 Server リソースキット*。 また、リソースキットでは、Url への印刷に関連するセキュリティ方法をシステム管理者が制御する方法についても説明します。

 

 




