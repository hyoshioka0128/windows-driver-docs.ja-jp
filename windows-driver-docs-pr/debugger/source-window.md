---
title: WinDbg でのソース コードのデバッグ
description: WinDbg でのソース コードのデバッグ
ms.assetid: 0f939d29-0d90-442e-96d7-fe756b92a7da
keywords:
- デバッグ情報ウィンドウ、ソースウィンドウ
- ソースウィンドウ
- ソースデバッグ、ソースウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75289348fa8a46cde10ba8faf67d8ee0d962f8df
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323589"
---
# <a name="source-code-debugging-in-windbg"></a>WinDbg でのソース コードのデバッグ


## <a name="span-idddk_source_path_dbgspanspan-idddk_source_path_dbgspansource-path"></a><span id="ddk_source_path_dbg"></span><span id="DDK_SOURCE_PATH_DBG"></span>ソースパス


ソースパスでは、C ファイルとC++ソースファイルが配置されているディレクトリを指定します。 デバッガーでのソースコードの表示の詳細については、「[ソースコード](source-code.md)」を参照してください。

**注**   企業ネットワークに接続している場合は、移行元サーバーを使用するのが最も効率的な方法です。 ソースパス内で srv @ no__t 文字列を使用して、移行元サーバーを使用できます。 ソースサーバーの詳細については、「[ソースサーバーの使用](using-a-source-server.md)」を参照してください。

 

WinDbg でソースパスを制御するには、次のいずれかの操作を行います。

-   **[ファイル]** メニューの **[ソースファイルパス]** を選択するか、ctrl キーを押しながら P キーを押します。

-   [**Srcpath (ソースパスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを使用します。 移行元サーバーを使用している場合、 [ **(ソースサーバーを使用して) srcfix**](-srcfix---lsrcfix--use-source-server-.md)は少し簡単になります。

-   [**Lsrcpath (ローカルソースパスの設定)** ](-srcpath---lsrcpath--set-source-path-.md)コマンドを使用します。 移行元サーバーを使用している場合は、 [**lsrcfix (ローカルソースサーバーを使用)** ](-srcfix---lsrcfix--use-source-server-.md)が少し簡単になります。

-   デバッガーを起動するときに、 **-srcpath**または **-lsrcpath**コマンドラインオプションを使用します。 「 [**WinDbg のコマンドラインオプション**](windbg-command-line-options.md)」を参照してください。

-   デバッガーを開始する前に、\_NT @ no__t-1SOURCE @ no__t-2PATH[環境変数](environment-variables.md)を設定します。

## <a name="span-idopening_and_closing_source_filesspanspan-idopening_and_closing_source_filesspanspan-idopening_and_closing_source_filesspanopening-and-closing-source-files"></a><span id="Opening_and_Closing_Source_Files"></span><span id="opening_and_closing_source_files"></span><span id="OPENING_AND_CLOSING_SOURCE_FILES"></span>ソースファイルのオープンと終了


ソースファイルを直接開いたり閉じたりするには、次のいずれかの操作を行います。

-   **[ファイル]** メニューの **[ソースファイルを開く]** をクリックするか、CTRL キーを押しながら O キーを押します。 また、ツールバーの [ソースファイルを開く] ボタンをクリックすると、[オープンソースファイル] ボタン @ no__t のスクリーンショットを @no__t**開く**こともできます。

    **注**  when またはツールバーボタンを使用してソースファイルを開くと、そのファイルのパスが自動的にソースパスに追加されます。

     

-   **[ファイル]** メニューの **[現在のウィンドウを閉じる]** をクリックします。
-   ソースウィンドウの隅にある **[閉じる]** ボタンをクリックします。
-   **[ファイル]** メニューの **[最近使ったファイル]** をクリックして、WinDbg で最近開いた4つのソースファイルのいずれかを開きます。
-   [ **. Open (オープンソースファイル)** ](-open--open-source-file-.md)コマンドを入力します。
-   [**Lsf (ソースファイルの読み込みまたはアンロード)** ](lsf--lsf---load-or-unload-source-file-.md)コマンドを入力します。

## <span id="ddk_source_windows_dbg"></span><span id="DDK_SOURCE_WINDOWS_DBG"></span>


WinDbg では、ソースウィンドウには、デバッガーに読み込まれているソースファイルが表示されます。

### <a name="span-idopening_the_source_windowspanspan-idopening_the_source_windowspanopening-the-source-window"></a><span id="opening_the_source_window"></span><span id="OPENING_THE_SOURCE_WINDOW"></span>ソースウィンドウを開く

新しいソースファイルを読み込むと、デバッガーによってソースウィンドウが開きます。 開いているソースウィンドウを復元または切り替えるには、 **[ウィンドウ]** メニューに移動し、メニューの下部にあるウィンドウの一覧から選択します。

次のスクリーンショットは、ソースウィンドウの例を示しています。

![デバッガーに読み込まれているソースファイルを表示するソースウィンドウのスクリーンショット](images/window-source.png)

各ソースファイルは、独自のソースウィンドウに存在します。 各ソースウィンドウのタイトルは、ソースファイルの完全なパスです。

### <a name="span-idusing_the_source_windowspanspan-idusing_the_source_windowspanusing-the-source-window"></a><span id="using_the_source_window"></span><span id="USING_THE_SOURCE_WINDOW"></span>ソースウィンドウの使用

各ソースウィンドウには、1つのソースファイルのテキストが表示されます。 デバッガーでソースファイルを編集することはできません。 フォントおよびタブ設定の変更の詳細については、「[テキストプロパティの変更](changing-text-properties.md)」を参照してください。

各ソースウィンドウには、コマンドが追加されたショートカットメニューがあります。 メニューにアクセスするには、タイトルバーを右クリックするか、ウィンドウの右上隅の近くに表示されるアイコンをクリックします (![ソースウィンドウのツールバーのショートカットメニューを表示するボタンのスクリーンショット](images/window-source-icon.png)) を選びます。 次の一覧では、メニューコマンドの一部について説明します。

-   **命令ポインターを現在の行に設定**する命令ポインターの値を現在の行に対応する命令に変更します。 このコマンドは、Edit | を使用することと同じです。 [現在の命令](edit---set-current-instruction.md)コマンドを設定するか、CTRL + SHIFT + I キーを押します。

-   **このファイルを編集**すると、ソースファイルがテキストエディターで開きます。 エディターは、WinDiff エディターのレジストリ情報、または WINDBG @ no__t-0INVOKE @ no__t 環境変数の値によって決定されます。 たとえば、WINDBG @ no__t-0INVOKE @ no__t-1EDITOR の値が次のようになっている場合を考えてみます。

    ```console
    c:\my\path\myeditor.exe -file %f -line %l
    ```

    この場合、Myeditor は、現在のソースファイルの1から始まる行番号を開きます。 % L オプションは、行番号が1から始まる必要があることを示します。% f は、現在のソースファイルを使用する必要があることを示します。 その他の代替手段としては、行番号が0から始まることを示す% L と、現在のソースファイルを使用する必要があることを示す% p があります。

-   **[選択範囲の評価]** は、 C++現在選択されているテキストを式エバリュエーターで評価します。 結果は[コマンドウィンドウデバッガー](debugger-command-window.md)に表示されます。 選択したテキストに複数の行が含まれている場合は、構文エラーが発生します。 このコマンドは、Edit | を使用することと同じです。 [[選択範囲の評価](edit---evaluate-selection.md)] コマンド、CTRL + SHIFT + V キー、または[ **??(式C++の評価)** ](----evaluate-c---expression-.md)コマンドを引数として選択します。

-   **選択さ**れた種類を表示する選択されたオブジェクトのデータ型を表示します。 この表示は、デバッガーコマンドウィンドウに表示されます。 選択したテキストに複数のオブジェクトが含まれている場合は、構文エラーまたはその他の不規則な結果が表示されることがあります。 このコマンドは、Edit | を使用することと同じです。 [選択した種類](edit---display-selected-type.md)のコマンドを表示するか、CTRL + SHIFT + Y キーを押します。

-   **[選択したメモリウィンドウを開く]** 選択した式のアドレスから始まるメモリを表示する、新しい [ドッキングされたメモリ] ウィンドウを開きます。

-   選択したソーストークンを**ウォッチウィンドウに追加**してウォッチウィンドウに追加します。

-   **現在の行で逆アセンブル**を行うと、現在の行に対応する命令が [[逆アセンブル] ウィンドウ](disassembly-window.md)に表示されます。 選択した行がソースウィンドウと [逆アセンブル] ウィンドウで強調表示されますが、このコマンドは表示のみに影響します。命令ポインターは変更されません。 このコマンドがクリックされたときに逆アセンブリウィンドウが閉じている場合は、そのウィンドウが開きます。

-   **[ソース言語の選択]** プログラミング言語の一覧を表示します。 ソースファイルの生成に使用したプログラミング言語を選択し、 **[OK]** をクリックして、現在のソースウィンドウに対して基本的な構文の強調表示を有効にします。 現在のソースウィンドウで構文の強調表示を無効にするには **&lt;None @ no__t-2**を選択します。

### <a name="span-idsource_window_colors_and_hover_evaluationspanspan-idsource_window_colors_and_hover_evaluationspansource-window-colors-and-hover-evaluation"></a><span id="source_window_colors_and_hover_evaluation"></span><span id="SOURCE_WINDOW_COLORS_AND_HOVER_EVALUATION"></span>ソースウィンドウの色とホバー評価

デバッガーがソースファイル名の拡張子を認識している場合、ソースウィンドウには特定の構文要素が色で表示されます。 色をオフにするか変更するには、次の手順を実行します。

-   1つのウィンドウで構文の色をオフにするには、ソースウィンドウのショートカットメニューを開き、 **[ソース言語の選択]** をクリックし、[ **&lt;none @ no__t**] をクリックします。

-   すべてのソースウィンドウで構文の色をオフにするには、 **[表示]** メニューの **[オプション]** をクリックします。 次に、 **[ソース言語の解析]** チェックボックスをオフにします。

-   構文の色を変更するには、 **[表示]** メニューの **[オプション]** をクリックします。 次に、 **[色]** 領域で、構文要素を選択し、 **[変更]** ボタンをクリックして色を変更します。

-   強調表示に使用される解析方法は、ソースファイルのファイル拡張子に関連付けられているプログラミング言語によって決まります。 特定のファイル拡張子に関連付けられているプログラミング言語を変更するには、[[ソース言語用のファイル拡張子] ダイアログボックス](view---source-language-file-extensions.md)を使用します。 このダイアログボックスを開くには、 **[表示]** メニューの **[ソース言語ファイル拡張子]** をクリックします。

現在のプログラムカウンターを表す行が強調表示されます。 ブレークポイントが設定されている行も強調表示されます。

ソースウィンドウを選択し、マウスを使用してそのウィンドウ内のシンボルをポイントすると、シンボルが評価されます。 評価は、 [**dt (Display Type)** ](dt--display-type-.md)コマンドによって生成されるものと同じです。 この評価を非アクティブ化するには、 **[表示]** メニューの **[オプション]** をクリックします。 次に、[**ホバー時に評価**する] チェックボックスをオフにします。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースデバッグと関連コマンドの詳細については、「[ソースモードでのデバッグ](debugging-in-source-mode.md)」を参照してください。

 

 





