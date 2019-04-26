---
title: 国際対応の INF ファイルの作成
description: 国際対応の INF ファイルの作成
ms.assetid: 7c07c4de-4a0f-4555-b153-15307c76a2a3
keywords:
- INF ファイル WDK デバイスのインストール、国際対応
- 国際対応の INF ファイル WDK
- ロケールに固有の INF ファイル WDK
- WDK のロケール固有のドライバー ファイル
- WDK の Unicode の INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11b887103ebddb8d0962158f1fc40acdbfa9d4db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346202"
---
# <a name="creating-international-inf-files"></a>国際対応の INF ファイルの作成





国際市場向けのインストールを作成する場合は、ロケールに固有の INF ファイルを提供する必要がありますと、場合によっては、ロケール固有のドライバー ファイル。

国際市場で使用される INF ファイルを使用する必要があります**%** <em>strkey</em> **%** ユーザー表示可能なすべてのテキストのトークン。 文字列は、INF で定義されている**文字列**セクションで、これは通常、INF ファイルの末尾。

### <a name="locale-specific-inf-files"></a>ロケール固有の INF ファイル

いくつかのロケールをサポートする 1 つの INF ファイルを作成することも次のガイドラインに従って、ロケールごとに個別の INF ファイルを作成することができます。

- 1 つの国際 INF ファイルを作成するには、ロケール固有のセットを含める必要があります**文字列**。<em>LanguageID</em>セクションのリファレンス ページ」の説明に従って、 [ **INF 文字列セクション**](inf-strings-section.md)します。 すべての国際市場向けの 1 つのインストール メディアを指定する場合は、この手法を使用します。

  Windows 2000 以降のバージョンの Windows でインストールする場合、これは、国際市場をサポートするための推奨される方法です。

- ロケールごとに個別の INF ファイルを作成する以外のすべての必要なセクションと、エントリを含むメイン INF ファイルを起動、**文字列**セクション。 各ファイルがだけが含まれているファイルの 2 番目のセットを作成し、**文字列**サポートされているロケールのセクション。 ロケールに固有の INF ファイルを生成するには、各文字列ファイルでメイン ファイルを連結します。

  Windows 2000 以降のバージョンの Windows でインストールする場合、この手法を使用して、*のみ*の国際市場別のインストール メディアを指定する場合。 Windows で使用する INF ファイルを決定できないために、1 つのインストール メディア上の INF ファイルを特定のオペレーティング システムのバージョンでは、複数のバージョンを提供できません。

### <a name="locale-specific-versions-of-driver-files"></a>ロケール固有のバージョンのドライバー ファイル

Windows 2000 以降のバージョンの Windows のロケール固有のバージョンのドライバー ファイルを提供した場合は、そのロケールでは、各ファイルの各バージョンをマークします。 ロケール固有の言語に中立としてではないファイルをマークしてください。 リソース ファイルに次のマクロ定義を追加することで、これを行うことができます。

```cpp
#define VER_LANGNEUTRAL
```

この定義を含むプリプロセッサ ディレクティブの前に記述する必要があります*common.ver*します。

ファイルをコンパイルすた後には、それぞれがマークされている言語中立として次の手順に従ってを確認できます。

1.  Windows エクスプ ローラーでファイルを右クリックします。

2.  **[プロパティ]** を選択します。

3.  をクリックして、**バージョン**タブ。

**言語**での選択、**他のバージョン情報**ウィンドウには言語中立として、または特定のロケールの対象としたファイルを識別する値が含まれています。

など、配布メディアの別のロケール固有のサブディレクトリでロケールに固有のファイルを配置/*英語*と/*ドイツ語*します。 INF ファイルで、次の手順を実行します。

-   内で、 [ **INF SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)などの文字列キー トークンを使用して、ロケール固有のサブディレクトリを指定 **%localesubdir**します。

-   個別に提供[ **INF 文字列のセクションでは**](inf-strings-section.md) 、各言語の各セクションでは、適切なサブディレクトリ名の文字列を定義します。

例:

```cpp
[SourceDisksNames]
1=%DiskName%,,,%LocaleSubDir%

[SourceDisksFiles]
mysftwre.exe=1

[Strings]              ; No language ID implies English
DiskName="My Excellent Software"
LocaleSubDir="English"
[Strings.0407]         ; 0407 is the language ID for German
DiskName="Meine ausgezeichnete Software"
LocaleSubDir="German"
```

### <a name="creating-unicode-inf-files"></a>Unicode の INF ファイルを作成します。

ASCII 範囲外に文字が、INF ファイルに含まれるかどうか (つまり、0 ~ 127 の範囲外)、INF ファイルが Unicode 形式でなければなりません。 Unicode の INF ファイルを作成する方法の 1 つは、メモ帳などのアプリケーションを使用して、Unicode 形式で保存します。 Unicode 形式で、INF でない場合、Windows は、文字変換を現在のロケールを使用します。 INF ファイルは、Unicode 形式では、Windows は、完全な Unicode 文字セットを使用します。

メモ帳などの一部のアプリケーションでは、リトル エンディアンまたはビッグ エンディアン形式で Unicode ファイルを作成できます。 Windows では、いずれかの形式を使用する INF ファイルをサポートします。

 

 





