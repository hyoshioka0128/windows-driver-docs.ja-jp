---
title: 例外とイベントの制御
description: 例外とイベントの制御
ms.assetid: cc8067f3-07de-4ee2-b028-94f9ac088891
keywords:
- 例外
- 例外、概要
- 例外の処理
- イベント
- イベント, 概要
- イベントの処理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3006c8f18c409208c55e4dad83d33f5f437c88f0
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464354"
---
# <a name="controlling-exceptions-and-events"></a>例外とイベントの制御


## <span id="ddk_controlling_exceptions_and_events_dbg"></span><span id="DDK_CONTROLLING_EXCEPTIONS_AND_EVENTS_DBG"></span>


キャッチして、さまざまな方法でユーザー モードとカーネル モードのアプリケーションで例外を処理することができます。 アクティブなデバッガー、事後分析のデバッガー、または内部のエラー処理ルーチンは、例外を処理するすべての一般的な方法です。

これらのさまざまな例外ハンドラーの優先順位の詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

Microsoft Windows オペレーティング システムが例外を生成したアプリケーション例外を処理するために、デバッガーで許可する*分割*デバッガー。 これは、アプリケーションが停止し、デバッガーは、アクティブのようになります。 デバッガーは、何らかの方法で例外を処理し、または状況を分析します。 デバッガーのプロセスを終了または、そのことができますし、実行を再開します。

デバッガーでは、例外を無視し、アプリケーションを実行場合、オペレーティング システムは、デバッガーが存在しない場合、他の例外ハンドラーを探します。 例外が処理される場合は、アプリケーションの実行が継続します。 ただし、例外がハンドルされていないが残っている場合、デバッガーは、状況に対処する 2 番目のチャンスが付与されます。

### <a name="span-idusingthedebuggertoanalyzeanexceptionspanspan-idusingthedebuggertoanalyzeanexceptionspanusing-the-debugger-to-analyze-an-exception"></a><span id="using_the_debugger_to_analyze_an_exception"></span><span id="USING_THE_DEBUGGER_TO_ANALYZE_AN_EXCEPTION"></span>デバッガーを使用して例外を分析するには

例外またはイベントは、デバッガーを中断、ときに実行されているコードと、アプリケーションが使用しているメモリを確認するのにデバッガーを使用できます。 特定の量を変更またはアプリケーションの別の時点へのジャンプ、によって、例外の原因を削除できる可能性があります。

発行することによって、実行を再開することができます、 [ **gh (例外処理に進む)** ](gh--go-with-exception-handled-.md)または[ **gn (Go 処理されない例外で)** ](gn--gn--go-with-exception-not-handled-.md)コマンド。

発行した場合、 **gn**アプリケーション終了例外を処理するために、デバッガーの 2 番目のチャンス コマンド。

### <a name="span-idkernelmodeexceptionsspanspan-idkernelmodeexceptionsspankernel-mode-exceptions"></a><span id="kernel_mode_exceptions"></span><span id="KERNEL_MODE_EXCEPTIONS"></span>カーネル モード例外

カーネル モード コードで発生する例外はユーザー モード例外よりもより深刻です。 カーネル モードの例外が処理されない場合、[バグ チェック](bug-checks--blue-screens-.md)が発行されると、システムが停止します。

として、ユーザー モード例外には、システムのカーネル モードのデバッガーがアタッチされている場合、デバッガーに通知する前に、*バグ チェック画面*(とも呼ばれる、*ブルー スクリーン*) が表示されます。 デバッガーがアタッチされていない場合は、バグの確認画面が表示されます。 この場合、オペレーティング システムを作成、[クラッシュ ダンプ ファイル](crash-dump-files.md)します。

### <a name="span-idcontrollingexceptionsandeventsfromthedebuggerspanspan-idcontrollingexceptionsandeventsfromthedebuggerspancontrolling-exceptions-and-events-from-the-debugger"></a><span id="controlling_exceptions_and_events_from_the_debugger"></span><span id="CONTROLLING_EXCEPTIONS_AND_EVENTS_FROM_THE_DEBUGGER"></span>例外と、デバッガーからイベントを制御します。

特定の方法で指定された例外とイベントに対応するデバッガーを構成することができます。

デバッガーでは、例外またはイベントごとにブレーク状態を設定できます。

-   (「ファースト チャンス」) が発生するとすぐにイベント デバッガーに中断が発生ことができます。

-   イベントは、他のエラー ハンドラー (「もう一度」) に対応する機会が与えられている後中断できます。

-   イベントはメッセージを送信するには、デバッガーも実行を続行します。

-   デバッガーでは、イベントを無視できます。

デバッガーでは、各例外とイベントの処理のステータスも設定できます。 デバッガーでは、例外処理など、未処理の例外イベントを扱うことができます。 (もちろん、実際にはエラーではないイベントは不要な処理です。)

次のいずれかの方法では、中断状態と処理の状態を制御できます。

-   使用して、 [ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN**、または**SXI**コマンド、[デバッガー コマンドウィンドウ](debugger-command-window.md)します。

-   (CDB、NTSD)使用して、 **-x**、 **-xe**、 **-xd**、 **- xn**、または **-xi**オプション、 [ **コマンドライン**](cdb-command-line-options.md)します。

-   (CDB、NTSD、および KD)使用して、 **sxe**または**sxd**キーワード、 [Tools.ini](configuring-tools-ini.md)ファイル。

-   (WinDbg のみ)をクリックして[イベント フィルター](debug---event-filters.md)上、**デバッグ**を開く メニュー、**イベント フィルター**  ダイアログ ボックス、および必要なオプションを選択します。

**SX\\*** のコマンドを **-x\\*** コマンド ライン オプションは、および**sx\\*** Tools.ini キーワードは、通常、中断を設定指定したイベントの状態です。 追加することができます、 **-h**オプションを代わりに設定する処理の状態が発生します。

4 つの特別なイベントのコードがあります (**cc**、 **hc**、 **bpec**と**ssec**) を常に中断状態ではなくの処理状態を指定します。

使用して、最新の例外またはイベントを表示することができます、 [ **.lastevent (最後のイベントを表示)** ](-lastevent--display-last-event-.md)コマンド。

### <a name="span-idcontrollingbreakstatusspanspan-idcontrollingbreakstatusspancontrolling-break-status"></a><span id="controlling_break_status"></span><span id="CONTROLLING_BREAK_STATUS"></span>中断状態の制御

例外またはイベントの中断状態を設定すると、次のオプションを使用できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">状態の名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<strong>SXE</strong>または<strong>-xe</strong></td>
<td align="left"><p><strong>break</strong></p>
<p>(<strong>有効になっている</strong>)</p></td>
<td align="left"><p>この例外が発生したときに、ターゲットはすぐにデバッガーを中断します。 その他のエラー ハンドラーがアクティブ化される前に、この中断が発生します。 このメソッドが呼び出された<em>初回処理</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXD</strong>または<strong>-xd</strong></td>
<td align="left"><p><strong>2 番目のチャンスの中断</strong></p>
<p>(<strong>無効</strong>)</p></td>
<td align="left"><p>デバッガーは中断されませんこの種の初回例外 (ただし、メッセージが表示されます)。 その他のエラー ハンドラーは、この例外に対処できない、実行が停止され、ターゲットがデバッガーを中断します。 このメソッドが呼び出された<em>セカンド チャンス処理</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
<strong>SXN</strong>または<strong>-xn</strong></td>
<td align="left"><p><strong>出力</strong></p>
<p>(<strong>通知</strong>)</p></td>
<td align="left"><p>この例外が発生したときに、対象アプリケーションは中断されませんデバッガーにまったくです。 ただし、この例外のユーザーに通知するメッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p></p>
<strong>SXI</strong>または<strong>-xi</strong></td>
<td align="left"><p><strong>無視します。</strong></p></td>
<td align="left"><p>この例外が発生して、対象アプリケーションは、デバッガーを中断しませんメッセージは表示されません。</p></td>
</tr>
</tbody>
</table>

 

例外が期待しない場合、 **SX** \*を設定する対象のアプリケーションを 2 番目のチャンスにデバッガーを中断します。 イベントの既定の状態は、このトピックの次の「イベントの定義と既定値」セクションに表示されます。

WinDbg のグラフィカル インターフェイスを使用して、中断状態を設定する[イベント フィルター](debug---event-filters.md)上、**デバッグ**] メニューの [イベントの一覧から使用する] をクリックして、**イベント フィルター**ダイアログボックスを選び**有効**、**無効**、**出力**、または**無視**します。

### <a name="span-idcontrollinghandlingstatusspanspan-idcontrollinghandlingstatusspancontrolling-handling-status"></a><span id="controlling_handling_status"></span><span id="CONTROLLING_HANDLING_STATUS"></span>状態の処理を制御します。

すべてのイベントと見なされます、未処理を使用しない限り、 [ **gh (例外処理に進む)** ](gh--go-with-exception-handled-.md)コマンド。

使用しない限り、すべての例外をハンドルされていないェホロ、 [ **sx\\**  * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)コマンドと共に、 **-h**オプション。

さらに、 **SX** \*オプションは無効なハンドル、状態の処理のステータスを構成できます\_ブレークポイント break 手順についてとシングル ステップの例外。 (この構成は、中断、構成から独立した)。これらのイベントの名前はその中断状態を構成するときに**ch**、 **bpe**、および**sse**、それぞれします。 これらのイベントがという名前の処理のステータスを構成するときに**hc**、 **bpec**、および**ssec**、それぞれします。 (イベントの完全な一覧については、次の「イベントの定義と既定」のセクションを参照してください)。

CTRL + C イベントの処理のステータスを構成することができます (**cc**) が、その中断状態ではありません。 アプリケーションでは、CTRL キーを押しながら C キー イベントを受信する場合、アプリケーションは常には、デバッガーを中断します。

使用すると、 **SX** \*コマンドを**cc**、 **hc**、 **bpec**、および**ssec**イベント、または使用すると、 **SX** \*コマンドと共に、 **-h**オプション、例外を次の操作が行われます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">状態の名前</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SXE</strong></p></td>
<td align="left"><p><strong>処理</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときの処理と見なされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SXD、SXN、SXI</strong></p></td>
<td align="left"><p><strong>処理されていません。</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときに処理されないと見なされます。</p></td>
</tr>
</tbody>
</table>

 

WinDbg のグラフィカル インターフェイスを使用して状態の処理を設定する をクリックして[イベント フィルター](debug---event-filters.md)上、**デバッグ**] メニューの [イベントの一覧から使用する] をクリックして、**イベント フィルター**クリックしてダイアログ ボックスで、 **Handled**または**処理されない**します。

### <a name="span-idautomaticcommandsspanspan-idautomaticcommandsspanautomatic-commands"></a><span id="automatic_commands"></span><span id="AUTOMATIC_COMMANDS"></span>自動コマンド

デバッガーでは、イベントまたは例外がデバッガーにブレークを発生させる場合に自動的に実行されるコマンドを設定することもできます。 初回の break コマンド文字列とセカンド チャンス区切りのためのコマンド文字列を設定することができます。 これらの文字列を設定することができます、 [ **SX\\**  * ](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)コマンドまたは[デバッグ |イベント フィルター](debug---event-filters.md)コマンド。 各コマンド文字列は、セミコロンで区切られた複数のコマンドを含めることができます。

これらのコマンドは、中断状態に関係なく実行されます。 中断状態が「無視」の場合は、コマンドは、引き続き実行されます。 中断状態が"セカンド チャンス break"の場合は、最初の発生時に、その他の例外ハンドラーが関係する前に、初回コマンドが実行されます。 コマンド文字列がなどの実行コマンドで終了できる[ **g (移動)**](g--go-.md)、 [ **gh (例外処理に進む)**](gh--go-with-exception-handled-.md)、または[**gn (Go 処理されない例外で)**](gn--gn--go-with-exception-not-handled-.md)します。

### <a name="span-ideventdefinitionsanddefaultsspanspan-ideventdefinitionsanddefaultsspanevent-definitions-and-defaults"></a><span id="event_definitions_and_defaults"></span><span id="EVENT_DEFINITIONS_AND_DEFAULTS"></span>イベントの定義と既定の設定

中断状態または次の例外の処理状態を変更することができます。 既定の中断状態が示されます。

次の例外の既定の状態の処理は、「処理されない」常にします。 この状態を変更する方法について注意します。 この状態を「処理済み」に変更する場合は、この種類のすべての初回とセカンド チャンス例外が処理済みと見なされ、この構成では、すべての例外処理ルーチンをバイパスします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント コード</th>
<th align="left">説明</th>
<th align="left">既定の中断状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>asrt</strong></p></td>
<td align="left"><p>アサーション エラー</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Av</strong></p></td>
<td align="left"><p>アクセス違反</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dm</strong></p></td>
<td align="left"><p>データの不整合</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>dz</strong></p></td>
<td align="left"><p>0 による整数除算</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>c000008e</strong></p></td>
<td align="left"><p>0 による浮動小数点除算</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>eh</strong></p></td>
<td align="left"><p>C++ EH 例外</p></td>
<td align="left"><p>次の例外の中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>gp</strong></p></td>
<td align="left"><p>ガード ページ違反</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ii</strong></p></td>
<td align="left"><p>無効な命令</p></td>
<td align="left"><p>次の例外の中断</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iov</strong></p></td>
<td align="left"><p>整数のオーバーフロー</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ip</strong></p></td>
<td align="left"><p>ページ I/O エラー</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>isc</strong></p></td>
<td align="left"><p>無効なシステムの呼び出し</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lsq</strong></p></td>
<td align="left"><p>無効なロックのシーケンス</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sbo</strong></p></td>
<td align="left"><p>スタック バッファー オーバーフロー</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sov</strong></p></td>
<td align="left"><p>スタック オーバーフロー</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wkd</strong></p></td>
<td align="left"><p>デバッガーを起動します。</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>aph</strong></p></td>
<td align="left"><p>アプリケーションのハング</p>
<p>この例外がトリガーされるは、Windows オペレーティング システムは終了プロセスが応答を停止している場合 (つまり、<em>が停止している</em>)。</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>3c</strong></p></td>
<td align="left"><p>子アプリケーションの終了</p></td>
<td align="left"><p>次の例外の中断</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>chhc</strong></p></td>
<td align="left"><p>ハンドルが無効です。</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>数</em></p></td>
<td align="left"><p>番号付き例外</p></td>
<td align="left"><p>次の例外の中断</p></td>
</tr>
</tbody>
</table>

 

**注**  をオーバーライドすることができます、 **asrt**を使用して、特定のアドレスの状態を解除、 [ **ah (アサーションの処理)** ](ah--assertion-handling-.md)コマンド。 **Ch**と**hc**イベント コードを同じ例外を参照してください。 使用して、その中断状態の制御を行うときに**sx\* ch**します。 使用して、その処理の状態を制御しているときに**sx\* hc**します。

 

中断状態または次の例外の処理状態を変更することができます。 既定の中断状態が示されます。

次の例外の既定の状態の処理は常に「処理」します。 これらの例外は、デバッガーと通信するため、する変更しないでください通常の状態を「処理されない」。 この状態は、デバッガーはそれらを無視する場合は、例外をキャッチするには、他の例外ハンドラーをによりします。

アプリケーションは、DBG を使用できます\_コマンド\_例外 (**dbce**)、デバッガーとの通信にします。 この例外は、ブレークポイントに似ていますが、使用することができます、 **SX** \*この例外が発生したときに、特定の方法で応答するコマンド。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント コード</th>
<th align="left">説明</th>
<th align="left">既定の中断状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dbce</strong></p></td>
<td align="left"><p>特別なデバッガー コマンド例外</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>vcpp</strong></p></td>
<td align="left"><p>Visual C の特別な例外</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>wos</strong></p></td>
<td align="left"><p>WOW64 シングル ステップの例外</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wob</strong></p></td>
<td align="left"><p>WOW64 ブレークポイント例外-</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sse<br>ssec</strong></p></td>
<td align="left"><p>シングル ステップの例外</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bpe<br>bpec</strong></p></td>
<td align="left"><p>ブレークポイント例外</p></td>
<td align="left"><p>休憩</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>cce<br>cc</strong></p></td>
<td align="left"><p>CTRL + C または CTRL + BREAK</p>
<p>ターゲットがコンソール アプリケーションで、CTRL キーを押しながら C キーまたは CTRL + BREAK がそれに渡される場合は、この例外がトリガーされます。</p></td>
<td align="left"><p>休憩</p></td>
</tr>
</tbody>
</table>

 

**注**  上の表で最後の 3 つの例外がある 2 つの異なるイベント コード。 使用して、その中断状態の制御を行うときに**sse**、 **bpe**、および**cce**します。 使用して、それらの処理状態を制御しているときに**ssec**、 **bpec**、および**cc**します。

 

### <a name="span-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanspan-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanspan-idthefollowingexceptionsareusefulwhenyouaredebuggingmanagedcodespanthe-following-exceptions-are-useful-when-you-are-debugging-managed-code"></a><span id="The_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="the_following_exceptions_are_useful_when_you_are_debugging_managed_code."></span><span id="THE_FOLLOWING_EXCEPTIONS_ARE_USEFUL_WHEN_YOU_ARE_DEBUGGING_MANAGED_CODE."></span>次の例外は、マネージ コードをデバッグする場合に便利です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント コード</th>
<th align="left">説明</th>
<th align="left">既定の状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>clr</strong></p></td>
<td align="left"><p>共通言語ランタイム例外</p></td>
<td align="left"><p>次の例外の中断</p>
<p>処理されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>clrn</strong></p></td>
<td align="left"><p>共通言語ランタイム通知例外</p></td>
<td align="left"><p>次の例外の中断</p>
<p>Handled</p></td>
</tr>
</tbody>
</table>

 

次のイベントの中断状態を変更することができます。 これらのイベントは例外ではないため、その処理の状態は関係ありません。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">イベント コード</th>
<th align="left">説明</th>
<th align="left">既定の中断状態</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ser</strong></p></td>
<td align="left"><p>システム エラー</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>cpr</strong>[<strong>:</strong><em>Process</em>]</p></td>
<td align="left"><p>プロセスの作成</p>
<p>このイベントの中断状態の設定は、ユーザー モードのデバッグにのみ適用されます。 このイベントは、カーネル モードでは発生しません。</p>
<p>このイベントを制御するには、CDB、またはいずれかを使って、-o、WinDbg で子プロセスのデバッグを有効にした場合にのみ<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">コマンド ライン オプション</a></strong>または、 <strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">します。childdbg (子プロセスのデバッグ)</a></strong> コマンド。</p>
<p>プロセス名は、任意のファイル名拡張子とアスタリスクを含めることができます (<em>) またはワイルドカード文字として疑問符 (?)。 デバッガーは、最新のみを記憶<strong>cpr</strong>設定します。 別のプロセスの個別の設定はサポートされていません。 コロンまたはの間にスペースを含める<strong>cpr</strong>と<em>プロセス</em>します。</p>
<p>場合<em>プロセス</em>は省略すると、すべての子プロセスの作成に、設定が適用されます。</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>epr</strong>[<strong>:</strong><em>Process</em>]</p></td>
<td align="left"><p>プロセスの終了</p>
<p>このイベントの中断状態の設定は、ユーザー モードのデバッグにのみ適用されます。 このイベントは、カーネル モードでは発生しません。</p>
<p>このイベントを制御するには、CDB、またはいずれかを使って、-o、WinDbg で子プロセスのデバッグを有効にした場合にのみ<strong><a href="cdb-command-line-options.md" data-raw-source="[command-line option](cdb-command-line-options.md)">コマンド ライン オプション</a></strong>または、 <strong><a href="-childdbg--debug-child-processes-.md" data-raw-source="[.childdbg (Debug Child Processes)](-childdbg--debug-child-processes-.md)">します。childdbg (子プロセスのデバッグ)</a></strong> コマンド。</p>
<p>プロセス名は、任意のファイル名拡張子とアスタリスクを含めることができます (</em>) またはワイルドカード文字として疑問符 (?)。 デバッガーは、最新のみを記憶<strong>epr</strong>設定します。 別のプロセスの個別の設定はサポートされていません。 コロンまたはの間にスペースを含める<strong>epr</strong>と<em>プロセス</em>します。</p>
<p>場合<em>プロセス</em>は省略すると、すべての子プロセスが終了する設定が適用されます。</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ct</strong></p></td>
<td align="left"><p>スレッドの作成</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>et</strong></p></td>
<td align="left"><p>スレッドの終了</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ld</strong>[<strong>:</strong><em>Module</em>]</p></td>
<td align="left"><p>モジュールの読み込み</p>
<p>指定した場合<em>モジュール</em>、この名前のモジュールが読み込まれるときに中断が発生します。 <em>モジュール</em>名前またはモジュールのアドレス指定できます。 名前を使用すると場合、<em>モジュール</em>さまざまなワイルドカード文字と指定子を含めることができます。 (構文の詳細については、次を参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>。)。</p>
<p>デバッガーは、最新の l のみを記憶<strong>d</strong>設定します。 個別のモジュールの個別の設定はサポートされていません。 コロンまたはの間にスペースを含める<strong>%ld</strong>と<em>モジュール</em>します。</p>
<p>場合<em>モジュール</em>は省略すると、イベントがトリガーされた任意のモジュールが読み込まれるときにします。</p></td>
<td align="left"><p>出力</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ud</strong>[<strong>:</strong><em>Module</em>]</p></td>
<td align="left"><p>モジュールのアンロード</p>
<p>指定した場合<em>モジュール</em>、またはこのベースのアドレスに、この名前のモジュールが読み込まれると、中断が発生します。 <em>モジュール</em>名前またはモジュールのアドレス指定できます。 名前を使用すると場合、<em>モジュール</em>する正確な名前またはワイルドカード文字を含めることができます。 場合<em>モジュール</em>に正確な名前、ベース アドレスに現在のデバッガーのモジュールの一覧を使用して解決はすぐに、アドレスとして格納されます。 場合<em>モジュール</em>、ワイルドカード文字を含むアンロード イベントが発生した場合、後で一致するパターン文字列が保持されます。</p>
<p>まれには、デバッガーは、アンロード イベントの名前の情報はありませんし、ベース アドレスによってのみと一致します。 そのため場合、<em>モジュール</em>、ワイルドカード文字を含む、デバッガーは、任意のモジュールが読み込まれるときに、この特定のアンロードの場合と区切りの名前の一致を実行できません。</p>
<p>デバッガーは、最新のみを記憶<strong>ud</strong>設定します。 個別のモジュールの個別の設定はサポートされていません。 コロンまたはの間にスペースを含める<strong>ud</strong>と<em>モジュール</em>します。</p>
<p>場合<em>モジュール</em>は省略すると、イベントがトリガーされた任意のモジュールが読み込まれるときにします。</p></td>
<td align="left"><p>出力</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>out</strong>[<strong>:</strong><em>Output</em>]</p></td>
<td align="left"><p>ターゲット アプリケーションの出力</p>
<p>指定した場合<em>出力</em>中断は、指定したパターンに一致する出力を受信したときのみに発生します。 <em>出力</em>さまざまなワイルドカード文字と指定子を含めることができます。 (構文の詳細については、次を参照してください<a href="string-wildcard-syntax.md" data-raw-source="[String Wildcard Syntax](string-wildcard-syntax.md)">文字列のワイルドカード構文</a>。)。ただし、<em>出力</em>コロンまたはスペースを含めることはできません。 照合が大文字小文字が区別されません。 コロンが含まれて、間にスペースまたは<strong>アウト</strong>と<em>出力</em>します。</p></td>
<td align="left"><p>無視</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ibp</strong></p></td>
<td align="left"><p>最初のブレークポイント</p>
<p>(このイベントは対象のコンピュータを再起動した後と、デバッグ セッションの開始時に発生します。)</p></td>
<td align="left"><p><strong>ユーザー モード。</strong>中断します。 この状態を"Ignore"に変更するにを使用して、 <strong>-g</strong><a href="command-line-options.md" data-raw-source="[command-line option](command-line-options.md)">コマンド ライン オプション</a>します。</p>
<p><strong>カーネル モード。</strong>無視してください。 この状態は、さまざまな方法で"Enabled"に変更できます。 この状態を変更する方法の詳細については、次を参照してください。<a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">クラッシュし、ターゲット コンピューターを再起動</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>iml</strong></p></td>
<td align="left"><p>初期のモジュールの読み込み</p>
<p>(カーネル モードのみ)</p></td>
<td align="left"><p>無視してください。 この状態は、さまざまな方法で"Break"に変更できます。 この状態を変更する方法の詳細については、次を参照してください。<a href="crashing-and-rebooting-the-target-computer.md" data-raw-source="[Crashing and Rebooting the Target Computer](crashing-and-rebooting-the-target-computer.md)">クラッシュし、ターゲット コンピューターを再起動</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





