---
title: WinDbg でのソース コードのデバッグ
description: WinDbg でのソース コードのデバッグ
ms.assetid: 0f939d29-0d90-442e-96d7-fe756b92a7da
keywords:
- デバッグ情報のウィンドウ、ソース ウィンドウ
- ソース ウィンドウ
- ソースのソース ウィンドウをデバッグします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75289348fa8a46cde10ba8faf67d8ee0d962f8df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572885"
---
# <a name="source-code-debugging-in-windbg"></a>WinDbg でのソース コードのデバッグ


## <a name="span-idddksourcepathdbgspanspan-idddksourcepathdbgspansource-path"></a><span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>ソース パス


ソース パスは、C および C++ ソース ファイルが配置されるディレクトリを指定します。 デバッガーでソース コードを表示する方法の詳細については、次を参照してください。[ソース コード](source-code.md)します。

**注**  ソース サーバーを使用するソース ファイルにアクセスする最も効率的な方法は、企業ネットワークに接続している場合。 移行元サーバーを使用するには、srv を使用して\*ソース パス内の文字列。 移行元サーバーの詳細については、次を参照してください。[移行元サーバーを使用して](using-a-source-server.md)します。

 

WinDbg でソース パスを制御するには、次のいずれかの操作を行います。

-   選択**ソース ファイルのパス**から、**ファイル**メニューまたは ctrl キーを押しながら P キーを押します。

-   使用して、 [ **.srcpath (ソース パスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンド。 移行元サーバーを使用している場合[ **.srcfix (ソース サーバーを使用)** ](-srcfix---lsrcfix--use-source-server-.md)多少簡単になります。

-   使用して、 [ **.lsrcpath (ローカル ソース パスを設定する)** ](-srcpath---lsrcpath--set-source-path-.md)コマンド。 移行元サーバーを使用している場合[ **.lsrcfix (ローカル ソース サーバーを使用する)** ](-srcfix---lsrcfix--use-source-server-.md)多少簡単になります。

-   デバッガーを起動するときに使用して、 **- srcpath**または **- lsrcpath**コマンド ライン オプション。 参照してください[ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md)します。

-   デバッガーを開始する前に、設定、 \_NT\_ソース\_パス[環境変数](environment-variables.md)します。

## <a name="span-idopeningandclosingsourcefilesspanspan-idopeningandclosingsourcefilesspanspan-idopeningandclosingsourcefilesspanopening-and-closing-source-files"></a><span id="Opening_and_Closing_Source_Files"></span><span id="opening_and_closing_source_files"></span><span id="OPENING_AND_CLOSING_SOURCE_FILES"></span>ソース ファイルの開閉


ソース ファイルを直接開いたり閉じたりには、次のいずれかの操作を行います。

-   選択**ソース ファイルを開く**から、**ファイル**メニューのまたは CTRL + O キーを押します。 使用することも、**ソース ファイルを開く**ボタン (![オープン ソース ファイル ボタンのスクリーン ショット](images/tbopen.png)) ツールバー。

    **注**  ソース パスに、そのファイルのパスを自動的に追加ソース ファイルを開く、メニューまたはツールバーのボタンを使用するとします。

     

-   選択**現在ウィンドウを閉じる**から、**ファイル**メニュー。
-   をクリックして、**閉じる**ソース ウィンドウの隅にあるボタンをクリックします。
-   選択**最近使ったファイル**から、**ファイル**] メニューの [最近開いた WinDbg で次の 4 つのソース ファイルの 1 つを開きます。
-   入力、 [ **.open (ソース ファイルを開きます)** ](-open--open-source-file-.md)コマンド。
-   入力、 [ **(ロードまたはアンロード ソース ファイル) の lsf** ](lsf--lsf---load-or-unload-source-file-.md)コマンド。

## <span id="ddk_source_windows_dbg"></span><span id="DDK_SOURCE_WINDOWS_DBG"></span>


、WinDbg では、ソース ウィンドウには、デバッガーに読み込まれているソース ファイルが表示されます。

### <a name="span-idopeningthesourcewindowspanspan-idopeningthesourcewindowspanopening-the-source-window"></a><span id="opening_the_source_window"></span><span id="OPENING_THE_SOURCE_WINDOW"></span>ソース ウィンドウを開く

デバッガーは、新しいソース ファイルの読み込み時に、ソース ウィンドウを開きます。 復元するか、ソース ウィンドウを開くに切り替えてするには、**ウィンドウ**メニュー、メニューの下部にある windows の一覧から選択します。

次のスクリーン ショットでは、ソース ウィンドウの例を示します。

![デバッガーに読み込まれたソース ファイルを表示する、ソース ウィンドウのスクリーン ショット](images/window-source.png)

各ソース ファイルは、独自のソース ウィンドウに存在します。 各ソース ウィンドウのタイトルは、ソース ファイルの完全なパスです。

### <a name="span-idusingthesourcewindowspanspan-idusingthesourcewindowspanusing-the-source-window"></a><span id="using_the_source_window"></span><span id="USING_THE_SOURCE_WINDOW"></span>ソース ウィンドウを使用します。

各ソース ウィンドウには、1 つのソース ファイルのテキストが表示されます。 デバッガーでのソース ファイルを編集することはできません。 フォントとタブの設定を変更する方法についての詳細については、次を参照してください。[テキストのプロパティを変更する](changing-text-properties.md)します。

各ソース ウィンドウには、その他のコマンドをショートカット メニューがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅近くに表示されるアイコンをクリックします。![ソース ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/window-source-icon.png)). 次の一覧では、メニュー コマンドの一部について説明します。

-   **現在の行を一連の命令ポインター**現在の行に対応する命令を命令ポインターの値を変更します。 このコマンドを使用すると、[編集 |現在の命令セット](edit---set-current-instruction.md)コマンドまたは CTRL + SHIFT + I キーを押します。

-   **このファイルを編集**テキスト エディターでソース ファイルを開きます。 エディターは、WinDiff エディターのレジストリ情報、または、WINDBG の値にによって決まりますが\_INVOKE\_エディター環境変数。 たとえば、大文字と小文字と WINDBG の値\_INVOKE\_エディターは、次です。

    ```console
    c:\my\path\myeditor.exe -file %f -line %l
    ```

    この場合は、現在のソース ファイルの 1 から始まる行番号を Myeditor.exe が開きます。 %L オプションでは、その行番号も参照してください、1 から始まる %f では、現在のソース ファイルを使用することを示しますを示します。 その他の置換可能性含める %l は、その行を示す番号は 0 から始まると %p は、現在のソース ファイルを使用することも指定できます。

-   **選択範囲を評価**C++ の式エバリュエーターを使用して、現在選択されているテキストを評価します。 結果が表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 選択したテキストには、1 つ以上の行が含まれている場合は、構文エラーが発生します。 このコマンドを使用すると、[編集 |選択範囲を評価](edit---evaluate-selection.md)コマンド、CTRL + SHIFT + V を押すかを使用して、 [**いますか。(C++ の式の評価)** ](----evaluate-c---expression-.md)コマンド、引数として選択したテキストを実行します。

-   **選択した種類の表示**選択したオブジェクトのデータ型が表示されます。 この表示は、デバッガー コマンド ウィンドウに表示されます。 選択したテキストが 1 つのオブジェクトよりも多く含まれている、構文エラーやその他の不規則な結果が表示可能性があります。 このコマンドを使用すると、[編集 |選択した型の表示](edit---display-selected-type.md)コマンドまたは CTRL + SHIFT + Y キーを押します。

-   **開いているメモリ ウィンドウの選択**新しいドッキング メモリ ウィンドウが開き、選択した式のアドレスで始まるメモリを表示します。

-   **[ウォッチ] ウィンドウに選択を追加**ウォッチ ウィンドウに、選択したソース トークンを追加します。

-   **現在の行に逆アセンブル**に表示される現在の行に対応する命令により、[逆アセンブル ウィンドウ](disassembly-window.md)します。 ソース ウィンドウで、[逆アセンブル] ウィンドウで、選択した行が強調表示されますが、このコマンドは、表示のみを影響、命令ポインターは変更されません。 このコマンドがクリックされたときに逆アセンブル ウィンドウが閉じている場合は、開かれます。

-   **ソース言語を選択します。** プログラミング言語の一覧を表示します。 クリックして、ソース ファイルを生成するために使用するプログラミング言語を選択**OK**現在のソース ウィンドウの基本的な構文の強調表示を有効にします。 選択**&lt;None&gt;** 現在のソース ウィンドウの構文の強調表示を無効にします。

### <a name="span-idsourcewindowcolorsandhoverevaluationspanspan-idsourcewindowcolorsandhoverevaluationspansource-window-colors-and-hover-evaluation"></a><span id="source_window_colors_and_hover_evaluation"></span><span id="SOURCE_WINDOW_COLORS_AND_HOVER_EVALUATION"></span>ソース ウィンドウの色とホバーの評価

デバッガーがソース ファイル名拡張子を認識しない場合、ソース ウィンドウの色で特定の構文要素が表示されます。 オフにするか、色を変更する、次の操作を行います。

-   1 つのウィンドウで、構文の色をオフに、ソース ウィンドウのショートカット メニューを開く をクリックして**ソース言語を選択します。**、順にクリックします **&lt;None&gt;** します。

-   すべてのソース ウィンドウの構文の色をオフに次のように選択します。**オプション**から、**ビュー**メニュー。 オフにし、**ソース言語の解析**チェック ボックスをオンします。

-   構文の色を変更するには、次のように選択します。**オプション**から、**ビュー**メニュー。 次に、**色**領域で、構文要素を選択し、をクリックして、**変更**色を変更するボタンをクリックします。

-   強調表示に使用する解析メソッドは、ソース ファイルのファイル拡張子に関連付けられているプログラミング言語によって決まります。 特定のファイル拡張子に関連付けられているプログラミング言語を変更するには、使用、[ソースの言語 ダイアログ ボックスのファイル拡張子](view---source-language-file-extensions.md)します。 このダイアログ ボックスを開くには、次のように選択します。**ソース言語のファイル拡張子**から、**ビュー**メニュー。

現在のプログラム カウンターを表す線が強調表示されます。 ブレークポイントが設定される行はも強調表示されます。

ソース ウィンドウを選択し、そのウィンドウ内のシンボルの上にマウスを使用すると、シンボルが評価されます。 評価がによって生成されるのと同じ、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。 この評価を非アクティブ化するには、**オプション**から、**ビュー**メニュー。 オフにし、**ホバー Evaluate**チェック ボックスをオンします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースのデバッグと関連するコマンドの詳細については、次を参照してください。[元のモードでデバッグ](debugging-in-source-mode.md)します。

 

 





