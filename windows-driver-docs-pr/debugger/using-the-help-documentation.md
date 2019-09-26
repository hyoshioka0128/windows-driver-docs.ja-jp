---
title: ヘルプ ドキュメントの使用
description: ヘルプ ドキュメントの使用
ms.assetid: ad826f45-3bad-4e10-811f-26ebf4f06c4d
keywords:
- HTML ヘルプ
- ヘルプファイルの検索
- ヘルプファイルのインデックス
- ヘルプファイルのお気に入り
- ヘルプファイルからのトピックの印刷
- hh.exe
- ヘルプファイル
- ヘルプファイル、概要
- ヘルプファイル、検索
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0969639f95a4c2033d02b517ebe96131c977c32
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284885"
---
# <a name="using-the-help-documentation"></a>ヘルプ ドキュメントの使用


## <span id="ddk_using_the_help_file_dbg"></span><span id="DDK_USING_THE_HELP_FILE_DBG"></span>


お読みの WinDbg ヘルプドキュメントは、Windows 用デバッグツールのパッケージに関するドキュメントです。

このドキュメントでは、Microsoft HTML ヘルプ (hh) に付属しているビューアーを使用します。 このビューアーには目次とインデックスが用意されており、ドキュメントの検索、お気に入りまたは頻繁に使用されるトピックの表示、および1つ以上のトピックの印刷を行うことができます。

このトピックの次のセクションでは、の機能と、ヘルプドキュメントの使用方法について説明します。

### <a name="span-idcontents_tabspanspan-idcontents_tabspancontents-tab"></a><span id="contents_tab"></span><span id="CONTENTS_TAB"></span>[目次] タブ

**[目次]** タブには、ドキュメントの目次の展開可能なビューが表示されます。

ノードの横にある **+** プラス記号 () をクリックするか、ノードのタイトルをダブルクリックして、そのノードの下にある目次を展開または縮小します。

### <a name="span-idindex_tabspanspan-idindex_tabspanindex-tab"></a><span id="index_tab"></span><span id="INDEX_TAB"></span>[インデックス] タブ

**[インデックス]** タブには、このドキュメントで使用されている用語の完全なインデックスが表示されます。 語句の先頭を入力するか、スクロールバーを使用してこのインデックスを検索することができます。

### <a name="span-idsearch_tabspanspan-idsearch_tabspansearch-tab"></a><span id="search_tab"></span><span id="SEARCH_TAB"></span>[検索] タブ

**[検索]** タブでは、ドキュメントに含まれている単語や語句を検索できます。 すべてのテキストを検索することも、検索範囲をトピックのタイトルに限定することもできます。

複数の単語を含む語句を検索するには、語句を引用符で囲みます。 複数の単語と語句は、AND、OR、および NOT 演算子で連結できます。 既定の演算子はとです。

"AND NOT" は無効であることに注意してください。 *Y*ではなく*x*を含むトピックを検索するには、"*x* not *y*" を使用します。 検索で NEAR を使用することもできます。

ワイルドカード文字も使用できます。 任意の1文字を表すには疑問符 ( **?** )、0個以上 **\*** の文字を表すにはアスタリスク () を使用します。 ただし、引用符で囲まれた文字列内では、ワイルドカード文字は使用できません。

すべての文字と数字は文字どおりに扱われますが、一部の記号は検索では使用できません。

検索では、指定した条件に一致するすべてのトピックの一覧が返されます。 [**前の結果を検索**する] ボックスを選択した場合は、これらの結果を検索してさらに条件を確認できます。

### <a name="span-idfavorites_tabspanspan-idfavorites_tabspanfavorites-tab"></a><span id="favorites_tab"></span><span id="FAVORITES_TAB"></span>[お気に入り] タブ

**[お気に入り]** タブでは、よくアクセスされるトピックのタイトルを保存できます。 トピックを表示しているときに、 **[お気に入り]** タブをクリックし、 **[追加]** ボタンをクリックします。

お気に入りの一覧でページの名前を変更するには、名前を2回クリックして、名前を再入力します。 お気に入り の一覧でトピックを表示するには、その名前をダブルクリックするか、1回クリックして **表示** をクリックします。 お気に入り の一覧からトピックを削除するには、1回クリックしてから **削除** をクリックします。

### <a name="span-idprinting_topicsspanspan-idprinting_topicsspanprinting-topics"></a><span id="printing_topics"></span><span id="PRINTING_TOPICS"></span>印刷に関するトピック

1つ以上のトピックを印刷するには、 **[コンテンツ]** タブのトピックをクリックし、ツールバーの **[印刷]** ボタンをクリックします。 選択したトピック、またはそのトピックとそのすべてのサブトピックのみを印刷するかどうかを確認するメッセージが表示されます。

表示しているトピックを印刷するには、表示 ウィンドウ内で右クリックし、ショートカットメニューの **印刷** をクリックします。 ただし、この方法を使用してサブトピックを印刷することはできません。

### <a name="span-idsearching_within_a_topicspanspan-idsearching_within_a_topicspansearching-within-a-topic"></a><span id="searching_within_a_topic"></span><span id="SEARCHING_WITHIN_A_TOPIC"></span>トピック内を検索する

表示しているトピック内のテキスト文字列を検索するには、CTRL キーを押しながら F キーを押すか、または **[編集]** メニューの**このトピックの [検索**] をクリックします。

### <a name="span-idaccessing_the_help_documentationspanspan-idaccessing_the_help_documentationspanaccessing-the-help-documentation"></a><span id="accessing_the_help_documentation"></span><span id="ACCESSING_THE_HELP_DOCUMENTATION"></span>ヘルプドキュメントへのアクセス

このヘルプドキュメントを開くには、次のいずれかの操作を行います。

-   **[スタート]** をクリックし、 **[すべてのプログラム]** 、 **[Windows 用デバッグツール]** の順にポイントして、 **[ヘルプのデバッグ]** をクリックします。

-   Windows エクスプローラーを開き、デバッガーの .chm ファイルを見つけて、ダブルクリックします。

-   コマンドプロンプトで、Debugger が格納されているフォルダーを参照し、 **hh debugger. .chm**を実行します。

-   任意の Windows デバッガーで、 [ **. hh (HTML ヘルプファイルを開く)** ](-hh--open-html-help-file-.md)コマンドを使用します。

-   WinDbg で、**ヘルプ** メニューの **コンテンツ** をクリックします。 このコマンドを実行すると、ヘルプドキュメントが開き、 **[コンテンツ]** タブが開きます。

-   WinDbg で、**ヘルプ** メニューの **インデックス** をクリックします。 このコマンドを実行すると、ヘルプドキュメントが開き、 **[インデックス]** タブが開きます。

-   WinDbg で、**ヘルプ** メニューの **検索** をクリックします。 このコマンドを実行すると、ヘルプドキュメントが開き、 **[検索]** タブが開きます。

-   WinDbg の多くのダイアログボックスには、 **[ヘルプ]** ボタンがあります。 **[ヘルプ]** をクリックしてこのドキュメントを開き、関連するページを開きます。

 

 





