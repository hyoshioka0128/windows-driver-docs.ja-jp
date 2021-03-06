---
title: アプリケーションから URL に印刷する
description: アプリケーションから URL に印刷する
ms.assetid: bc9aedb4-1d64-4b70-b14b-1392f914a635
keywords:
- インターネット Url への印刷、WDK の印刷
- 印刷キューの URL によって特定された WDK
- WDK プリンターの表示名
- WDK の Url への印刷
- Web ページの Url への印刷、WDK を印刷します。
- Web ページの WDK プリンター、Url への印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d099985ded26f5e03fa83da22de7946948b81878
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390275"
---
# <a name="printing-to-urls-from-applications"></a>アプリケーションから URL に印刷する





アプリケーションの観点からは、URL によって特定された印刷キューに印刷は、UNC によって特定された印刷キューへの出力と同じです。 アプリケーションは、URL によって印刷キューにアクセスすることは知りませんが。

によって[印刷の Web ページの閲覧](viewing-print-web-pages.md)ユーザーはインストールして、URL によって特定された印刷キューに接続します。 この場合、印刷キューには、同じ「表示名」プリント サーバーに、このフレンドリ名は、ユーザーの印刷のフォルダーに表示が割り当てられます。

アプリケーション通常を参照して印刷キュー、フレンドリ名によって UNC によって特定された印刷キューのようにします。 呼び出し、**ようになりました**(原因となった、たとえば、GDI の呼び出しを行うアプリケーションで) ローカルの印刷プロバイダー、関数がフレンドリ名が含まれます。 さらに、ローカルの印刷プロバイダーを呼び出す**ようになりました**HTTP の印刷プロバイダー (Inetpp.dll)、印刷キューの URL を指定します。

フレンドリ名での印刷キューを参照しているアプリケーションは、ローカルまたはネットワークでは、印刷キューはかどうか、またはネットワーク プロトコルは、RPC、SMB、または HTTP かどうかの一般的に対応していません。 ただしアプリケーションは、必要に応じて、呼び出す**ようになりました**を直接 URL を指定します。 URL を指定する場合**ようになりました**、次の URL 形式を使用する必要があります。

http://&lt;ServerName&gt;/printers/&lt;ShareName&gt;/.printer

場所&lt;ServerName&gt; (インターネット接続の DNS 名をまたはイントラネット接続の WINS の名前)、サーバー名は、「プリンター」は、サーバー上の仮想ディレクトリを表すと&lt;ShareName&gt;が、そのプロパティ シートで指定されている、印刷キューの共有名。 (仮想ディレクトリは、Microsoft Windows SDK のドキュメントで説明しますが)。

クライアントのスプーラー コンポーネントまたはアプリケーションを呼び出すと**ようになりました**などのスプーラー関数では、後続の呼び出し、URL を指定して**StartDocPrinter**、 **WritePrinter**、これには、クライアントの HTTP の印刷プロバイダーによって処理されます。 HTTP の印刷プロバイダーは、URL に引数を追加し、プリント サーバーに結果として得られる URL 文字列を送信します。

Url を含む印刷要求を受け入れるための Microsoft Windows 2000 プリント サーバーを実行しなければなりませんか。

-   Microsoft インターネット インフォメーション サーバー (IIS) での Windows 2000 Server ソフトウェア、または

-   Microsoft ピアの Web サーバーで Windows 2000 Professional ソフトウェア

Url を含む印刷要求を受け入れるための Windows XP プリント サーバーを実行しなければなりませんか。

-   Microsoft Windows Server 2003 のソフトウェア Microsoft インターネット インフォメーション サーバー (IIS) で、または

-   Microsoft ピアの Web サーバーで Windows XP Professional ソフトウェア

**注**   A Windows XP Home の Edition のプリント サーバーは、Url を含む要求を受け付けることができません。

 

プリント サーバー、IIS またはピアの Web サーバーは、URL 文字列を受け取ります。 Inetpp.dll でクライアント システム上の文字列に追加の引数には、サーバーによって Msw3prt.dll に含まれている HTTP のプリント サーバーの呼び出しがあります。 HTTP のプリント サーバーは、プリンターの RAW 形式のデータを受け取り、ローカルの印刷スプーラーに送信します。

プリンター データは、インターネット印刷プロトコル (IPP 1.0) で、プリンターの操作グループ (PWG) Internet Engineering Task Force (IETF) の定義を使用してサーバーにクライアントから送信されます。

クライアント URL によって特定された印刷キューに印刷する場合、次の図は、サーバーの印刷スプーラーにクライアント アプリケーションから印刷データを取得するパスを示します。

![url によって特定された印刷キューへの出力を示す図](images/prntpath.png)

クライアントとサーバーは、Windows 2000 またはそれ以降のシステムを示すようには場合、RPC プロトコルは通常 (が常にではありません) 使用クライアント サーバー間の通信。 (詳細については、次を参照してください[Web ページから印刷ドライバーをインストールする](installing-print-drivers-from-a-web-page.md)。)。クライアントとサーバーの Windows 2000 またはそれ以降のシステムの両方でない場合は、HTTP が使用されます。 HTTP は、プリンター用内部のネットワーク カードを含めることし IPP 1.0 をサポートしているサーバーに接続されていないためにも使用されます。

プリント サーバーのセキュリティは、プリント サーバーを実行するには、IIS によって提供されます。 IIS でサポートされているセキュリティ メカニズムが記載されて、 *IIS リソース ガイド*に含まれている、* *

*Microsoft Windows 2000 Server Resource Kit*します。 さらに、リソース キットでは、具体的にはどのようにシステム管理者を制御できます Url への出力に関連付けられているセキュリティ メソッドについて説明します。

 

 




