---
title: トレース メッセージの一覧の機能
description: トレース メッセージの一覧の機能
ms.assetid: c640626d-6d64-45c4-861f-6e2f20b7dfb1
keywords:
- トレース メッセージの一覧 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5912df03c0a6c848fe9dd5f5d73698b796fca06a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549891"
---
# <a name="trace-message-list-features"></a>トレース メッセージの一覧の機能


このトピックでは、トレース メッセージの一覧の機能について説明します。 これらの機能を使用して、一覧をカスタマイズすることができます。

### <a name="span-iddisplayingandhidingcolumnsspanspan-iddisplayingandhidingcolumnsspandisplaying-and-hiding-columns"></a><span id="displaying_and_hiding_columns"></span><span id="DISPLAYING_AND_HIDING_COLUMNS"></span>表示と列を非表示

表示すると、トレース メッセージの一覧の列を非表示は、列見出しを右クリックします。 ショートカット メニューが表示されたら、確認のプロパティが表示されます。unchecked プロパティは表示されません。 または、プロパティを非表示には、ショートカット メニューから選択します。

この手順を使用すると、メッセージを生成したソース コードで関数名と行番号を含むメッセージをトレースに関する重要な情報を表示します。

### <a name="span-idsavingthecolumnconfigurationspanspan-idsavingthecolumnconfigurationspansaving-the-column-configuration"></a><span id="saving_the_column_configuration"></span><span id="SAVING_THE_COLUMN_CONFIGURATION"></span>列の構成を保存しています

Traceview では、既定で選択した列を表示します。 たい場合は、別の列が表示され、非表示になって、構成を保存する、列として新しい既定の構成。

新しい列の構成を保存するには、次の操作を行います。

1.  トレース メッセージの一覧で、任意の列見出しを右クリックします。

2.  クリックして**既定値として保存**します。

### <a name="span-idsortingbycolumnspanspan-idsortingbycolumnspansorting-by-column"></a><span id="sorting_by_column"></span><span id="SORTING_BY_COLUMN"></span>列で並べ替え

列の値を並べ替えるには、列見出しをクリックします。 列見出しを繰り返しをクリックすると、列を昇順と降順の列の値の順序の間で切り替えます。 既定では、トレース メッセージの一覧が値で並べ替えられた、 **Msg\#** 列。

### <a name="span-idautofitcolumnsspanspan-idautofitcolumnsspanautofit-columns"></a><span id="autofit_columns"></span><span id="AUTOFIT_COLUMNS"></span>Autofit 列

その列のデータの幅には、各列の幅を調整するには、トレース メッセージの任意の行 (列見出し) 以外のトレース メッセージの一覧を右クリックし、クリックして**AutoFit 列**します。

### <a name="span-idcleardisplayspanspan-idcleardisplayspanclear-display"></a><span id="clear_display"></span><span id="CLEAR_DISPLAY"></span>表示をクリアします。

すべてのトレース メッセージを削除、表示から、トレース メッセージの任意の行 (列見出し) 以外のトレース メッセージの一覧を右クリックし、クリックして**クリア表示**します。

表示をオフにするとは、トレース メッセージはトレース ログまたは出力ファイルから削除されません。 ただし、メッセージがリアルタイムのトレース セッションによって生成されているログまたは出力ファイルに保存されていない場合、それらを復元することはできません。

### <a name="span-idcopyingtracemessagesspanspan-idcopyingtracemessagesspancopying-trace-messages"></a><span id="copying_trace_messages"></span><span id="COPYING_TRACE_MESSAGES"></span>トレース メッセージのコピー

トレース メッセージの一覧からトレース メッセージをコピーするには、次の操作を行います。

1.  コピーするトレース メッセージを選択します。 Shift キーを押しながらクリックを使用すると、連続していないメッセージをコピーするのにには、連続するメッセージまたは ctrl キーを押しながらクリックを選択します。

2.  Ctrl キーを押しながら C キーを押します。 または、選択したトレース メッセージの任意のセルを右クリックし、クリックして**コピー**します。

メッセージは、タブ区切り形式でコピーされます。 テキスト ファイルまたは後で使用するためのスプレッドシート ファイルに貼り付けることができます。

トレース メッセージを保存する方法の詳細については、次を参照してください。[トレース ログのテキストのバージョンを作成する](creating-text-versions-of-trace-logs.md)します。

 

 





