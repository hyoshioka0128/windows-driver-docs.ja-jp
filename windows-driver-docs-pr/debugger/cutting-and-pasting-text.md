---
title: テキストの切り取りと貼り付け
description: テキストの切り取りと貼り付け
ms.assetid: efc62bee-ba35-4bff-b88b-3b287ededc38
keywords:
- テキストの切り取り
- テキストを貼り付ける
- テキストをコピーします。
- デバッグ情報のウィンドウ、カット アンド ペースト テキスト
- text
- テキストの編集
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bff0bfa7a3e076a9cb311bb8f91b8b0a404324b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374443"
---
# <a name="cutting-and-pasting-text"></a>テキストの切り取りと貼り付け


## <span id="ddk_cutting_and_pasting_text_dbg"></span><span id="DDK_CUTTING_AND_PASTING_TEXT_DBG"></span>


WinDbg では、テキストとはあまり知られていないいくつかのメソッドの操作の多くの一般的なメソッドを使用します。

### <a name="span-idselectingtextspanspan-idselectingtextspanselecting-text"></a><span id="selecting_text"></span><span id="SELECTING_TEXT"></span>テキストを選択します。

内のテキストを選択する、[ソース ウィンドウ](source-window.md)で、[逆アセンブル ウィンドウ](disassembly-window.md)のいずれかのウィンドウで、[デバッガー コマンド ウィンドウ](debugger-command-window.md)、またはダイアログ ボックスでは、キーを押して、テキストの一方の端をポイントしてマウスの左ボタンを押し、他のテキストの末尾にポインターをドラッグします。

ウィンドウですべてのテキストを選択するには、クリックしての[すべて選択](edit---select-all.md)上、**編集**メニューまたは ctrl キーを押しながら A キーを押します。

[コール スタック ウィンドウ](calls-window.md)、ウォッチ ウィンドウ、 [[ローカル] ウィンドウ](locals-window.md)、 [[レジスタ] ウィンドウ](registers-window.md)、および[メモリ ウィンドウ](memory-window.md)、任意の範囲を選択することはできません、テキストの行全体を選択したりできますセルします。 目的の行またはそのテキストを選択するセルをクリックします。

テキストを入力する際は、それぞれ、カーソルの左側、右側にテキストを削除する削除し、BACKSPACE キーを押します。 テキストを選択した場合は、選択項目を削除するこれらのキーを押すことができます。 テキストを選択し、任意の文字を入力すると、選択した新しい文字に置き換えます。

### <a name="span-idcopyingtextspanspan-idcopyingtextspancopying-text"></a><span id="copying_text"></span><span id="COPYING_TEXT"></span>テキストをコピーします。

テキストをコピーし、そのテキストを選択し、次のいずれかの操作を行います。

-   マウスの右ボタンを押します。 (このメソッドは、いくつかの場所でのみ機能します。 マウスの右ボタンを使用する方法の詳細については、参照してください、右マウス ボタンをクリックします。)

-   Ctrl キーを押しながら C キーを押します。

-   Ctrl キーを押しながら INSERT キーを押します。

-   (ドッキングしてタブ付き windows のみ)クリックして**コピー**上、**編集**メニュー。

-   をクリックして、**コピー (Ctrl + C)** ボタン (![コピー ボタンのスクリーン ショット](images/tbcopy.png)) ツールバー。

### <a name="span-idcuttingtextspanspan-idcuttingtextspancutting-text"></a><span id="cutting_text"></span><span id="CUTTING_TEXT"></span>テキストの切り取り

テキストを切り取ってクリップボードに移動して、テキストを選択し、次のいずれかの操作を行います。

-   Ctrl キーを押しながら X キーを押します。

-   SHIFT + DEL キーを押します。

-   (ドッキングしてタブ付き windows のみ)をクリックして**切り取り**上、**編集**メニュー。

-   をクリックして、**切り取り (Ctrl + X)** ボタン (![切り取りのボタンのスクリーン ショット](images/tbcut.png)) ツールバー。

デバッガー コマンド ウィンドウの下部のペイン、ウォッチ ウィンドウの左の列と任意のダイアログ ボックスでテキストを切り取ることができます (つまり、任意の場所からサポートするテキストを入力)。

### <a name="span-idpastingtextspanspan-idpastingtextspanpasting-text"></a><span id="pasting_text"></span><span id="PASTING_TEXT"></span>テキストを貼り付ける

クリップボードからテキストを貼り付けるには、カーソルがテキストを挿入します (または置換するテキストを選択) にして、次のいずれかの操作を配置します。

-   マウスの右ボタンを押します。 (このメソッドがいくつかの場所でのみ機能し、このメソッドを使用してテキストを置換することはできません。 詳細は、このメソッドを使用する方法についてを参照してください、右マウス ボタンをクリックします。)

-   Ctrl キーを押しながら V キーを押します。

-   Shift キーを押しながら INSERT キーを押します。

-   (ドッキングしてタブ付き windows のみ)をクリックして**貼り付け**上、**編集**メニュー。

-   をクリックして、**貼り付け (CTRL + V)** ボタン (![貼り付け ボタンのスクリーン ショット](images/tbpaste.png))、tooblar でします。

デバッガー コマンド ウィンドウの下部のペインに、ウォッチ ウィンドウの左の列に、および任意のダイアログ ボックスにテキストを貼り付けることができます (つまり、任意の場所にサポートするテキストを入力)。

### <a name="span-idrightmousebuttonspanspan-idrightmousebuttonspanright-mouse-button"></a><span id="right_mouse_button"></span><span id="RIGHT_MOUSE_BUTTON"></span>マウスの右ボタン

マウスの右ボタンが可能なコピーと貼り付け大幅に短縮いくつかの効果があります。

-   デバッガー コマンド ウィンドウのいずれかのウィンドウ、スクラッチ パッド、逆アセンブル ウィンドウで、または任意のソース ウィンドウでテキストを選択すると、マウスの右ボタンを押し、テキストがクリップボードにコピーします。 ただし場合、**簡易編集モード**でが選択解除された[ビュー |オプション](view---options.md)、これらの場所を右クリックして、現在の場所に最も関連するメニューが表示されます。

-   デバッガー コマンド ウィンドウのいずれかのウィンドウで、スクラッチ パッド、または ウォッチ ウィンドウのテキスト入力領域に、(任意のテキストを選択) せずにカーソルを移動して、マウスの右ボタンを押し、クリップボードの内容がウィンドウに貼り付けられます。 ただし場合、**簡易編集モード**でが選択解除された[ビュー |オプション](view---options.md)、これらの場所を右クリックして、現在の場所に最も関連するメニューが表示されます。

-   任意のボックスにカーソルを置き、マウスの右ボタンを持つメニュー キーを押しますして**を元に戻す**、**切り取り**、**コピー**、**貼り付け**、および**すべて選択**オプションが表示されます。 これらのオプションを選択することができます。

 

 





