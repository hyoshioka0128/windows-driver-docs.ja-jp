---
title: 東アジアしてを NTF ファイルに変換します。
description: 東アジアしてを NTF ファイルに変換します。
ms.assetid: 0932068a-9101-4cdc-8c80-b2d3a4b507ba
keywords:
- ミニドライバー WDK Pscript、して変換します。
- NTF ファイル
- .ntf ファイル
- .afm ファイル
- して
- ファイルの WDK Pscript NTF してに変換します。
- Adobe フォント メトリック WDK Pscript
- WDK の東アジア言語フォントを印刷します。
- WDK のアジア言語フォントを印刷します。
- 簡体字フォントは、WDK の印刷をサポートします。
- 繁体字中国語フォントは、WDK の印刷をサポートします。
- WDK の日本語フォントのサポート
- 韓国語のフォントのサポートの WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef9272459d5353a20f2273779bb596627aeb207e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531642"
---
# <a name="converting-east-asian-afm-files-to-ntf-files"></a>東アジアしてを NTF ファイルに変換します。





東アジア フォントの .afm ファイルを Makentf.exe を処理する (で説明した[NTF ファイルへの変換 AFM ファイル](converting-afm-files-to-ntf-files.md)) のフォント、CID (文字 ID) を Unicode からマッピング テーブルを作成する .map と .ps ファイルが必要です。

東アジア .afm ファイルは、CID の説明と、フォントに含まれる各グリフのメトリックを持ちます。 Unicode コードとフォントの文字セットの文字コードを対応する .map ファイルが一覧表示します。 .Ps ファイルには、Unicode コードの一覧が含まれていて、フォントの文字に対応する Cid を設定します。

以降、東アジア .afm ファイルでは、Makentf.exe は文字セットを決定します。 文字セットに基づき、Makentf.exe は、該当する .map と .ps ファイルを検索します。 Makentf.exe は、.map ファイルからのフォントで使用できる Unicode コードを一覧します。 Unicode コード リスト .ps ファイルから Makentf.exe は、フォントの Unicode の CID をマッピング テーブルを作成します。 現時点では、.afm ファイルを使用して、フォントの各 CID (グリフ) が実際に含まれることを確認します。 .Afm ファイル内の CID が見つかった場合は、マッピング テーブルに CID を Unicode コードからマッピング エントリが作成されます。 マッピング エントリは、CID が見つからない場合は作成されません。

簡体字、繁体字中国語、日本語、および韓国語の .ntf ファイルを作成するために必要な .map と .ps ファイルは、以下の一覧に表示されます。 これらのファイルおよび .afm ファイルを同じディレクトリに配置します。

### <a name="chinese-simplified"></a>簡体字中国語

-   ucs2gbk.map

-   unigbh.ps

-   unigbv.ps

### <a name="chinese-traditional"></a>繁体字中国語

-   ucs2bg5.map

-   unicnsh.ps

-   unicnsv.ps

### <a name="japanese"></a>Japanese

-   ucs283h.map

-   ucs283v.map

-   ucs2msj.map

-   uni83h.ps

-   uni83v.ps

-   unijish.ps

-   unijisv.ps

### <a name="korean"></a>韓国語

-   ucs2jhb.map

-   ucs2uhc.map

-   uniksh.ps

-   uniksv.ps

 

 




