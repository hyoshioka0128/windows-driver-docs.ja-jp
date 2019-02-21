---
title: プリンターの種類のページをインストールします。
description: プリンターの種類のページをインストールします。
ms.assetid: 6c878612-d490-4791-a284-c48f1db0cde8
keywords:
- カスタマイズされた印刷 Web ページ WDK をインストールします。
- カスタマイズされた印刷の Web ページ、WDK をインストールします。
- 特定のプリンターのインストール WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d0e18e5b38f8469feecd934b0f6620a7b69ec0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559133"
---
# <a name="installing-pages-for-a-printer-type"></a>プリンターの種類のページをインストールします。





プリンターの標準の TCP/IP ポート モニタを使用する場合は、プリンターの種類に固有のプリンターの詳細ページをインストールできます。 これを行うに (.gif ファイルやリンク先のページの ASP ファイル)、すべての従属ファイルと共に、ページの ASP ファイルを含める、[プリンター INF ファイル](printer-inf-files.md)のプリンターの種類。 プリンター INF ファイルのセクションの例を次に示します。

```cpp
[Manufacturer]
"ACME"
 
[ACME]
"ACME Mega Laser" = ACML01.PPD
 
[ACML01.PPD]
CopyFiles=@ACML01.PPD,PSCRIPT,ACML1WEB
DataSection=PSCRIPT_DATA
 
[ACML1WEB]
PAGE1.ASP, ACML1.ASP ;ACML1.ASP renamed to PAGE1.ASP during installation
ACML2.ASP
ACGF001.GIF
 
[DestinationDirs]
DefaultDestiDir=66000
ACML1WEB=66004
```

クラスのインストーラーをプリンターには、この INF ファイルのセクションが検出されるには、次の操作を行います。

-   として書式設定されたディレクトリを作成&lt;ルート&gt;\\&lt;製造元&gt;\\&lt;プリンターの種類&gt;します。 例については、次のサブディレクトリが作成します。

    ..\\ACME\\ACME メガ レーザー

-   Acml1.asp、Asml2.asp、および Acgf001.gif をサブディレクトリにコピーします。

-   Acml1.asp を Page1.asp (ACML1WEB セクションの最初のステートメントによって生じた) に変更します。

Page1.asp ファイル名の前に、例に示すように表示するのには、最初の ASP ファイルを識別する必要がありますに注意してください。 インストーラーでは、先のディレクトリで、このファイルを Page1.asp に変更します。

ページの形式ですべての ASP ファイル名*N*.asp、場所*N*は 1、2、3、Microsoft によって予約されています。

サンプルの INF ファイルが付属、[サンプル ASP ファイル](sample-asp-files.md)Windows Driver Kit でします。

 

 




