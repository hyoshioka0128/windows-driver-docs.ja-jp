---
title: 製造元のページをインストールします。
description: 製造元のページをインストールします。
ms.assetid: 637b265f-9138-4696-b52a-ce63cd1f2c01
keywords:
- カスタマイズされた印刷 Web ページ WDK をインストールします。
- カスタマイズされた印刷の Web ページ、WDK をインストールします。
- プリンターの製造元に固有のインストール WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b4b9ef2c8eac102fefef5b8530e60005aadd69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552995"
---
# <a name="installing-pages-for-a-manufacturer"></a>製造元のページをインストールします。





製造元固有の標準の TCP/IP ポート モニタを使用して、製造元のすべてのプリンターの種類では、プリンターの詳細ページをインストールすることができます。 これを行うには、製造元のサブディレクトリに (.gif ファイルやリンク先のページの ASP ファイル)、すべての従属ファイルと共に、ページの ASP ファイルを配置 (\\%windir%\\web\\プリンター\\ &lt;製造元&gt;)。 これを実現する、カスタマイズされたセットアップ プログラムを指定する必要があります。

ページの初期の ASP ファイルは、Page1.asp を名前する必要があります。 ページの形式ですべての ASP ファイル名*N*.asp、場所*N*は 1、2、3、Microsoft によって予約されています。

標準の TCP/IP ポート モニタを使用して、プリンターの種類に固有のページはありませんが、製造元のプリンターの種類のすべては、製造元固有のページを使用します。

システムは、インストール時にプリンターの INF ファイルを読み取ることによって、プリンターの製造元を決定します。 ユーザーがプリンターの詳細ページを表示しようとすると、システムに Page1.asp という名前のファイルが存在するかどうかにまず&lt;ルート&gt;\\&lt;製造元&gt;\\&lt;プリンター型&gt;します。 ファイルが見つからない場合、システムがチェック&lt;ルート&gt;\\&lt;製造元&gt;します。

 

 



