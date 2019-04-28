---
title: プリンターの詳細ページが表示されます。
description: プリンターの詳細ページが表示されます。
ms.assetid: f7824350-a6de-45ca-8d72-859edf77e86d
keywords:
- 特定のページの閲覧、WDK 印刷の Web ページのカスタマイズ
- プリンターの詳細ページを表示します。
- プリンターの詳細ページを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76ee8a17f7f05bff893d255ad4f4ef469f2d7791
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370626"
---
# <a name="which-printer-details-page-is-displayed"></a>どのプリンター詳細ページが表示されていますか?





ユーザーがプリンターの詳細ページを表示しようとした場合、サーバーは、ASP ファイルを読み取るを判断、次のアルゴリズムを使用します。

-   標準の TCP/IP ポート モニタを使用して、プリンターに: 場合
    1.  サーバーは、まず、プリンターの種類に固有の ASP ファイルのセットがインストールされているかどうかを確認します。 そうである場合に使用されます。
    2.  プリンターの種類に固有の ASP ファイルが使用できない場合、サーバーは、一連の製造元に固有の ASP ファイルがインストールされているかどうかを確認します。 そうである場合に使用されます。
    3.  製造元に固有の ASP ファイルが使用可能なない場合、およびプリンターの snmp プリンター MIB (RFC 1759) がサポートされている場合は、Microsoft の既定の ASP ファイルが使用されます。
    4.  SNMP がサポートされていない場合、プリンターの詳細ページが指定されていません。
-   プリンターに標準の TCP/IP ポート モニタを使用しない場合、サーバーを監視に固有の ASP ファイルのセットがインストールされているかどうかを確認します。 そうである場合に使用されます。 それ以外の場合は、プリンターの詳細ページが指定されていません。

詳細については、次を参照してください。[印刷 Web ページをカスタマイズしたインストール](installing-customized-print-web-pages.md)します。

 

 




