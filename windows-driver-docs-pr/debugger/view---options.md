---
title: ビューのオプション
description: ビューのオプション
ms.assetid: 2579c586-f1f3-4b03-a47f-22be98fe6c51
keywords:
- ビューのオプション
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86859d492f81fa532a600f5835b7623f586230fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536790"
---
# <a name="view--options"></a>ビュー |オプション


## <span id="ddk_view_options_dbg"></span><span id="DDK_VIEW_OPTIONS_DBG"></span>


をクリックして**オプション**上、**ビュー**を開く メニュー、**オプション** ダイアログ ボックス。 このコマンドを実行 ボタンをクリックすると (![オプション ボタンのスクリーン ショット](images/tbopt.png)) ツールバー。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

**オプション** ダイアログ ボックスで選択するか、次のオプションの選択を解除することができます。

<span id="Tab_width"></span><span id="tab_width"></span><span id="TAB_WIDTH"></span>**タブの幅**  
**タブ幅**ボックスは、任意のソース ウィンドウでタブ文字を表示する方法を制御します。 **タブ幅**ボックスに、各タブの設定との間に空白の数を入力します。 (既定の設定では 8 です。 テキスト プロパティの詳細については、次を参照してください[テキストのプロパティを変更する](changing-text-properties.md)。)。

<span id="Reuse_after_opening_this_many"></span><span id="reuse_after_opening_this_many"></span><span id="REUSE_AFTER_OPENING_THIS_MANY"></span>**この数を開いた後で再利用します。**  
**この数を開いた後、再利用**ボックスは、同時に開くことができるドキュメント、またはソースの windows の数を制御します。 ソース ウィンドウの指定した数に達している場合は、既存のウィンドウを閉じると、新しいウィンドウを開きます。 タブのドッキングのターゲットを閉じないでくださいとしてマークされている Windows。 最後の windows を閉じるには、最も最近使用したものです。

<span id="Parse_source_languages"></span><span id="parse_source_languages"></span><span id="PARSE_SOURCE_LANGUAGES"></span>**ソース言語を解析します。**  
場合、**ソース言語を解析** チェック ボックスが選択されているすべてのソース ウィンドウ内のソース コードのテキストは、ソースの構文の単純な解析に合わせて色付けされます場合、。 色を変更する、**色**、ダイアログ ボックスの領域が構文要素を選択し、クリックして**変更**します。 (構文の色をオフに 1 つのソース ウィンドウで、そのウィンドウのショートカット メニューを開き、をクリックして**ソース言語を選択します**、 をクリックし、  **&lt;None&gt;**。)。

<span id="Evaluate_on_hover"></span><span id="evaluate_on_hover"></span><span id="EVALUATE_ON_HOVER"></span>**ポインターを合わせると評価します。**  
場合、**ポインターを合わせると評価** チェック ボックスが選択されている (および**ソース言語を解析**もチェック ボックスをオン)、ウィンドウを選択しをポイントすると、ソース ウィンドウ内のシンボルが評価される、マウスを使用して記号です。 評価がによって生成されるのと同じ、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

<span id="Enter_repeats_last_command"></span><span id="enter_repeats_last_command"></span><span id="ENTER_REPEATS_LAST_COMMAND"></span>**繰り返しの最後のコマンドを入力します。**  
場合、 **」と入力は、最後のコマンドを繰り返す** チェック ボックスが選択されているプロンプトで、空で ENTER キーを押すことができます場合、[デバッガー コマンド ウィンドウ](debugger-command-window.md)を前のコマンドを繰り返します。 このチェック ボックスをオフにした場合、ENTER キーは新しいプロンプトを生成します。

<span id="Automatically_scroll"></span><span id="automatically_scroll"></span><span id="AUTOMATICALLY_SCROLL"></span>**自動スクロールします。**  
**自動スクロール** チェック ボックスは、デバッガー コマンド ウィンドウに新しいテキストが送信されるときに発生する自動スクロールを制御します。 この機能を無効にする場合は、オフ、**自動スクロール**チェック ボックスをオンします。 このスクロールの詳細については、次を参照してください。[デバッガー コマンドを使用して](using-debugger-commands.md)します。

<span id="Workspace_Prompts"></span><span id="workspace_prompts"></span><span id="WORKSPACE_PROMPTS"></span>**ワークスペースのプロンプト**  
**ワークスペースにメッセージが表示されます**領域で、クリックできます WinDbg でワークスペースを保存するタイミングと頻度を決定する 3 つのオプションのいずれか。

-   クリックすると**常に確認**ワークスペースの変更 (デバッグ セッションが終了する) など、デバッガーを表示するときに、**ワークスペースの保存** ダイアログ ボックスのワークスペースを保存することができます。

    **ワークスペースの保存** ダイアログ ボックスをクリックすると**今後表示しない**、WinDbg のリセット、**ワークスペースにメッセージが表示されます**オプションを**保存しない**または**常に保存**します。

-   クリックすると**常に保存**、変更されるたびに、ワークスペースが自動的に保存されます。

-   クリックすると**保存しない**ワークスペースは、変更し、保存には求められませんは保存されません。

<span id="QuickEdit_Mode"></span><span id="quickedit_mode"></span><span id="QUICKEDIT_MODE"></span>**簡易編集モード**  
場合、**簡易編集モード** チェック ボックスを選択すると、コピーまたは貼り付け、ウィンドウの選択状態に応じて項目を右クリックすることができます。 このチェックをオフにすると、簡易編集モードが無効になり、ウィンドウのショートカット メニューを開き、項目を右クリックすることができます。 さまざまな設定を個々 の windows に与えることはできません。簡易設定は、すべての windows にグローバルに適用されます。 既定では、このボックスがオンにします。 簡易設定は、現在のワークスペースに保存されます。

<span id="Colors"></span><span id="colors"></span><span id="COLORS"></span>**色**  
表示されるソース テキストの色を変更するから項目を選択、**色**領域およびクリック**変更**します。 色を選択またはカスタムの色を選択してクリックして**OK**します。

**色**メニューで、次の項目の色を変更することができます。

-   最初の 10 個の項目のテキストを表す、[逆アセンブル ウィンドウ](disassembly-window.md)と[ソース ウィンドウ](source-window.md)します。

-   **データのテキストを変更**項目が変更されているデータのエントリを表します (たとえば、 [[レジスタ] ウィンドウ](registers-window.md))。

-   10**ソース** *Xxx*項目がソース ウィンドウ内の要素の構文を使用する色を制御します。

-   残りの項目は、さまざまな種類のデバッガー コマンド ウィンドウでテキストを参照してください。

これらの変更を有効するときに色をクリックする**OK**します。 これらの変更を破棄するには、次のようにクリックします。**キャンセル**します。

 

 





