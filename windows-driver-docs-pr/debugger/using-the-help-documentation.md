---
title: ヘルプ ドキュメントの使用
description: ヘルプ ドキュメントの使用
ms.assetid: ad826f45-3bad-4e10-811f-26ebf4f06c4d
keywords:
- HTML ヘルプ
- ヘルプ ファイルの検索
- ヘルプ ファイルのインデックス
- ヘルプ ファイルでのお気に入り
- ヘルプ ファイルからのトピックの印刷
- hh.exe
- ヘルプ ファイル
- ヘルプ ファイルの概要
- ヘルプ ファイルを検索
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f4da4720ead1e1c9f04a32cae1e02968525286e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571421"
---
# <a name="using-the-help-documentation"></a>ヘルプ ドキュメントの使用


## <span id="ddk_using_the_help_file_dbg"></span><span id="DDK_USING_THE_HELP_FILE_DBG"></span>


読み取りを行っている WinDbg ヘルプ ドキュメントでは、Windows のツールをデバッグ パッケージのドキュメントです。

このドキュメントでは、Microsoft HTML ヘルプ (hh.exe) で指定されているビューアーを使用します。 このビューアーは、内容とインデックスのテーブルを提供します。 またはドキュメント内を検索、お気に入りをマークすることができますとトピック、および印刷の 1 つまたは複数のトピックを頻繁に使用します。

このトピックでは、次のセクションでは、機能とヘルプ ドキュメントを使用する方法について説明します。

### <a name="span-idcontentstabspanspan-idcontentstabspancontents-tab"></a><span id="contents_tab"></span><span id="CONTENTS_TAB"></span>[目次] タブ

**内容**タブには、ドキュメントの目次の拡張可能な表示。

プラス記号をクリックします (**+**) ノードの横にあるかを拡張または縮小、そのノードの下の目次ノードのタイトルをダブルクリックします。

### <a name="span-idindextabspanspan-idindextabspanindex-tab"></a><span id="index_tab"></span><span id="INDEX_TAB"></span>インデックス タブ

**インデックス**タブには、このドキュメントで使用される用語の完全なインデックスが表示されます。 用語の先頭を入力するか、スクロール バーを使用して、このインデックスを検索します。

### <a name="span-idsearchtabspanspan-idsearchtabspansearch-tab"></a><span id="search_tab"></span><span id="SEARCH_TAB"></span>[検索] タブ

**検索** タブで、任意の単語またはドキュメントに含まれている語句を検索することができます。 すべてのテキストを検索したり、トピック タイトルに検索を制限できます。

1 つ以上の単語を含む語句を検索するには、語句を引用符で囲みます。 複数の単語や語句を接続するには、AND と OR、および NOT 演算子。 既定の演算子は。

「AND NOT"が無効であるに注意してください。 含むトピックを検索する*x*なく*y*を使用して、"*x*いない*y*"。 検索で、NEAR を使用することもできます。

ワイルドカード文字は使用もします。 疑問符 () を使用して (**?**) を表す任意の 1 文字と、アスタリスク (* *\\* * *) 0 個以上の文字を表します。 ただし、引用符で囲まれた文字列内のワイルドカード文字を使用することはできません。

すべての文字と数字は文字どおり、扱われますが、一部のシンボルの検索では許可されません。

検索では、指定した条件に一致するすべてのトピックの一覧を返します。 選択した場合、**前の結果を検索**ボックスで、詳細な条項のこれらの結果を検索できます。

### <a name="span-idfavoritestabspanspan-idfavoritestabspanfavorites-tab"></a><span id="favorites_tab"></span><span id="FAVORITES_TAB"></span>[お気に入り] タブ

**お気に入り** タブで、一般的にアクセスしたトピックのタイトルを保存することができます。 トピックを表示しているときに、クリックして、**お気に入り** タブをクリックして、**追加**ボタンをクリックします。

お気に入りの一覧で、ページの名前を変更するには、は、その名前 2 回を緩やかに変化をクリックし、新しい名前を入力します。 トピックをお気に入りの一覧を表示する名前をダブルクリックします。 または 1 回 をクリックをクリック**表示**します。 お気に入りの一覧からトピックを削除、1 回クリックし、順にクリックします**削除**します。

### <a name="span-idprintingtopicsspanspan-idprintingtopicsspanprinting-topics"></a><span id="printing_topics"></span><span id="PRINTING_TOPICS"></span>トピックを印刷します。

1 つまたは複数のトピックを印刷するには、トピックをクリックして、**内容** タブをクリックして、**印刷**ツールバーのボタンをクリックします。 求められます選択したトピックのみまたはそのトピックとサブトピックのすべてを印刷するかどうか。

ビュー ウィンドウ内で右クリックして表示しているトピックを印刷することもできます。**印刷**ショートカット メニューの します。 ただし、このメソッドでは、サブトピックの印刷するためはありません。

### <a name="span-idsearchingwithinatopicspanspan-idsearchingwithinatopicspansearching-within-a-topic"></a><span id="searching_within_a_topic"></span><span id="SEARCHING_WITHIN_A_TOPIC"></span>トピック内の検索

表示されているトピック内のテキスト文字列を検索するには、ctrl キーを押しながら F キーを押しますまたは をクリックして**このトピックで**上、**編集**メニュー。

### <a name="span-idaccessingthehelpdocumentationspanspan-idaccessingthehelpdocumentationspanaccessing-the-help-documentation"></a><span id="accessing_the_help_documentation"></span><span id="ACCESSING_THE_HELP_DOCUMENTATION"></span>ヘルプ ドキュメントにアクセスします。

このヘルプ ドキュメントを開くには、次のいずれかの操作を行います。

-   をクリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**ツールを Windows のデバッグ**、順にクリックします**ヘルプ デバッグ**。

-   Windows エクスプ ローラーを開き Debugger.chm ファイルを探し、それをダブルクリックします。

-   コマンド プロンプトで Debugger.chm と実行を含むフォルダーを参照**hh debugger.chm**します。

-   任意の Windows デバッガーで使用して、 [ ***.hh* (開いている HTML ヘルプ ファイル)** ](-hh--open-html-help-file-.md)コマンド。

-   、WinDbg で次のようにクリックします。**内容**上、**ヘルプ**メニュー。 このコマンドを開きのヘルプ ドキュメントが開き、**内容**タブ。

-   、WinDbg で次のようにクリックします。**インデックス**上、**ヘルプ**メニュー。 このコマンドを開きのヘルプ ドキュメントが開き、**インデックス**タブ。

-   、WinDbg で次のようにクリックします。**検索**上、**ヘルプ**メニュー。 このコマンドは、ヘルプを表示し、開きます、**検索**タブ。

-   WinDbg で多くのダイアログ ボックスが**ヘルプ**ボタン。 クリックして**ヘルプ**をこのドキュメントを開き、該当するページを開きます。

 

 





