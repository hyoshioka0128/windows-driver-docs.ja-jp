---
title: シンボルのオプション
description: シンボルのオプション
ms.assetid: 4a501ea3-431c-4c11-8826-154eb8799a64
keywords:
- シンボル、シンボルのオプションの設定
- シンボル、SYMOPT_XXXX
- ノイズの多いシンボルの読み込み
- CV レコード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9832b751affe05bd31977c0a82280a3e2f692e7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335514"
---
# <a name="symbol-options"></a>シンボルのオプション


## <span id="ddk_setting_symbol_options_dbg"></span><span id="DDK_SETTING_SYMBOL_OPTIONS_DBG"></span>


さまざまなオプションは、シンボルが読み込まれ、使用方法の制御に使用できます。 これらのオプションは、さまざまな方法で設定できます。

次の表では、これらのシンボル オプションを示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">オプション名</th>
<th align="left">既定のデバッガー</th>
<th align="left">既定の DBH</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p><a href="#symopt-case-insensitive" data-raw-source="[SYMOPT_CASE_INSENSITIVE](#symopt-case-insensitive)">SYMOPT_CASE_INSENSITIVE</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p><a href="#symopt-undname" data-raw-source="[SYMOPT_UNDNAME](#symopt-undname)">SYMOPT_UNDNAME</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p><a href="#symopt-deferred-loads" data-raw-source="[SYMOPT_DEFERRED_LOADS](#symopt-deferred-loads)">SYMOPT_DEFERRED_LOADS</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p><a href="#symopt-no-cpp" data-raw-source="[SYMOPT_NO_CPP](#symopt-no-cpp)">SYMOPT_NO_CPP</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p><a href="#symopt-load-lines" data-raw-source="[SYMOPT_LOAD_LINES](#symopt-load-lines)">SYMOPT_LOAD_LINES</a></p></td>
<td align="left"><p>KD、CDB でオフ</p>
<p>On in WinDbg</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p><a href="#symopt-omap-find-nearest" data-raw-source="[SYMOPT_OMAP_FIND_NEAREST](#symopt-omap-find-nearest)">SYMOPT_OMAP_FIND_NEAREST</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p><a href="#symopt-load-anything" data-raw-source="[SYMOPT_LOAD_ANYTHING](#symopt-load-anything)">SYMOPT_LOAD_ANYTHING</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80</p></td>
<td align="left"><p><a href="#symopt-ignore-cvrec" data-raw-source="[SYMOPT_IGNORE_CVREC](#symopt-ignore-cvrec)">SYMOPT_IGNORE_CVREC</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100</p></td>
<td align="left"><p><a href="#symopt-no-unqualified-loads" data-raw-source="[SYMOPT_NO_UNQUALIFIED_LOADS](#symopt-no-unqualified-loads)">SYMOPT_NO_UNQUALIFIED_LOADS</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p><a href="#symopt-fail-critical-errors" data-raw-source="[SYMOPT_FAIL_CRITICAL_ERRORS](#symopt-fail-critical-errors)">SYMOPT_FAIL_CRITICAL_ERRORS</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p><a href="#symopt-exact-symbols" data-raw-source="[SYMOPT_EXACT_SYMBOLS](#symopt-exact-symbols)">SYMOPT_EXACT_SYMBOLS</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p><a href="#symopt-allow-absolute-symbols" data-raw-source="[SYMOPT_ALLOW_ABSOLUTE_SYMBOLS](#symopt-allow-absolute-symbols)">SYMOPT_ALLOW_ABSOLUTE_SYMBOLS</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><a href="#symopt-ignore-nt-sympath" data-raw-source="[SYMOPT_IGNORE_NT_SYMPATH](#symopt-ignore-nt-sympath)">SYMOPT_IGNORE_NT_SYMPATH</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>SYMOPT_INCLUDE_32BIT_MODULES</p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4000</p></td>
<td align="left"><p><a href="#symopt-publics-only" data-raw-source="[SYMOPT_PUBLICS_ONLY](#symopt-publics-only)">SYMOPT_PUBLICS_ONLY</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8000</p></td>
<td align="left"><p><a href="#symopt-no-publics" data-raw-source="[SYMOPT_NO_PUBLICS](#symopt-no-publics)">SYMOPT_NO_PUBLICS</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10000</p></td>
<td align="left"><p><a href="#symopt-auto-publics" data-raw-source="[SYMOPT_AUTO_PUBLICS](#symopt-auto-publics)">SYMOPT_AUTO_PUBLICS</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オン</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000</p></td>
<td align="left"><p><a href="#symopt-no-image-search" data-raw-source="[SYMOPT_NO_IMAGE_SEARCH](#symopt-no-image-search)">SYMOPT_NO_IMAGE_SEARCH</a></p></td>
<td align="left"><p>オン</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000</p></td>
<td align="left"><p><a href="#symopt-secure" data-raw-source="[SYMOPT_SECURE](#symopt-secure)">SYMOPT_SECURE</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="even">
<td align="left"><p>これに対して、0x80000</p></td>
<td align="left"><p><a href="#symopt-no-prompts" data-raw-source="[SYMOPT_NO_PROMPTS](#symopt-no-prompts)">SYMOPT_NO_PROMPTS</a></p></td>
<td align="left"><p>KD、CDB で</p>
<p>WinDbg でオフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p><a href="#symopt-debug" data-raw-source="[SYMOPT_DEBUG](#symopt-debug)">SYMOPT_DEBUG</a></p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idchanging-the-symbol-option-settingsspanspan-idchanging_the_symbol_option_settingsspanchanging-the-symbol-option-settings"></a><span id="changing-the-symbol-option-settings"></span><span id="CHANGING_THE_SYMBOL_OPTION_SETTINGS"></span>シンボルのオプションの設定を変更します。

[ **.Symopt (シンボル オプションを設定する)** ](-symopt--set-symbol-options-.md)シンボルのオプション設定の表示を変更するコマンドを使用できます。 さらに、さまざまなコマンド ライン パラメーターおよびコマンドが使用するこれらの設定を変更するにはこれらは、個々 の SYMOPT に一覧表示\_*XXX*セクション。

一度にすべての設定を制御することも、 **- sflags**[コマンド ライン オプション](command-line-options.md)します。 始まる 16 進数または 10 進数では、このオプションの後にすることができます**0 x**します。 これにより正しく整列シンボルのフラグから 16 進数を使用することをお勧めします。 全体のビット フィールドを設定し、すべてのシンボルのハンドラーの既定値をオーバーライドするために、このメソッドを使用して注意します。 たとえば、 **sflags 0x401**しか入らない SYMOPT\_EXACT\_シンボルと SYMOPT\_ケース\_INSENSITIVE、ですが、通常は上にあるその他のすべてのオプションをオフにも既定値です。

合計フラグのビットの既定値は、WinDbg で 0x30237、し、KD、CDB で 0xB0227 で 0x10C13 [DBH ツール](dbh.md)、これらのプログラムがシンボルに関連するコマンド ライン オプションを指定せずに起動された場合。

### <a name="span-idsymopt-case-insensitivespanspan-idsymopt_case_insensitivespansymopt_case_insensitive"></a><span id="symopt-case-insensitive"></span><span id="SYMOPT_CASE_INSENSITIVE"></span>SYMOPT\_ケース\_INSENSITIVE

このシンボルのオプションではシンボルの名前を大文字をすべて検索します。

このオプションは、すべてのデバッガーで既定でオンです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x1**または .symopt 0x1 の場合、それぞれします。

このオプションは、DBH で既定でオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt +1 または symopt-1 の場合をそれぞれ使用します。

### <a name="span-idsymopt-undnamespanspan-idsymopt_undnamespansymopt_undname"></a><span id="symopt-undname"></span><span id="SYMOPT_UNDNAME"></span>SYMOPT\_UNDNAME

このシンボル オプションを指定する、表示されていると原因は、シンボルの装飾を無視するシンボル名の検索、装飾するパブリック シンボル名とします。 このオプションがアクティブかどうかに関係なく、このプライベート シンボルの名前が修飾されていることはありません。 シンボルの名前の装飾については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

このオプションは、すべてのデバッガーで既定でオンです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x2**または .symopt 0x2、それぞれします。

このオプションは、DBH で既定でオンです。 電源オフ、-d コマンド ライン オプションを使用する場合。 DBH が実行されていることができますにすることオンまたはオフ symopt +2 または symopt-2 をそれぞれ使用します。

### <a name="span-idsymopt-deferred-loadsspanspan-idsymopt_deferred_loadsspansymopt_deferred_loads"></a><span id="symopt-deferred-loads"></span><span id="SYMOPT_DEFERRED_LOADS"></span>SYMOPT\_延期\_読み込み

このシンボルのオプションの名前は*シンボルの読み込みの遅延*または*シンボルの遅延読み込み*します。 アクティブになっているときにシンボルが実際に読み込まれていないターゲット モジュールが読み込まれるときにします。 代わりに、必要とされるため、シンボルは、デバッガーによって読み込まれます。 詳細については、[シンボルの読み込みの遅延](deferred-symbol-loading.md)を参照してください。

このオプションは、すべてのデバッガーで既定でオンです。 CDB および KD では、秒のコマンド ライン オプションでは、このオプションをオフになります。 できますも無効にすることで CDB を使用して、 **LazyLoad**変数、 [tools.ini](configuring-tools-ini.md)ファイル。 デバッガーが実行されている場合、このオプションにできますオンまたはオフを使用して **.symopt + 0x4**または .symopt 0x4、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +4 または symopt-4 でをそれぞれ使用します。

### <a name="span-idsymopt-no-cppspanspan-idsymopt_no_cppspansymopt_no_cpp"></a><span id="symopt-no-cpp"></span><span id="SYMOPT_NO_CPP"></span>SYMOPT\_いいえ\_CPP

このシンボルのオプションは、C++ の変換をオフにします。 このシンボル オプションを設定すると、 **::** は置き換え **\_ \_** ですべてのシンボルです。

このオプションは既定ではすべてのデバッガーではオフです。 Snc-コマンド ライン オプションを使用して、それをアクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x8**または .symopt 0x8、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +8 または symopt である-8 をそれぞれ使用します。

### <a name="span-idsymopt-load-linesspanspan-idsymopt_load_linesspansymopt_load_lines"></a><span id="symopt-load-lines"></span><span id="SYMOPT_LOAD_LINES"></span>SYMOPT\_ロード\_行

このシンボルのオプションは、ソース ファイルから読み取る行番号情報を使用できます。 このオプションは、ソースが正常に動作するデバッグの上にする必要があります。

KD、CDB でこのオプションは既定で無効です。このオプションは、WinDbg で、既定でオンです。 KD、CDB で行コマンド ライン オプションではこのオプションを有効にします。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x10**または .symopt 0x10、それぞれします。 これも切り替えるできますオンとオフを使用して、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンド。

このオプションは、DBH で既定でオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt +10 または symopt、-10 をそれぞれ使用します。

### <a name="span-idsymopt-omap-find-nearestspanspan-idsymopt_omap_find_nearestspansymopt_omap_find_nearest"></a><span id="symopt-omap-find-nearest"></span><span id="SYMOPT_OMAP_FIND_NEAREST"></span>SYMOPT\_OMAP\_検索\_NEAREST

コードが最適化されているし、予期される場所でシンボルはありません、このオプションは、代わりに使用される最も近いシンボルとなります。

このオプションは、すべてのデバッガーで既定でオンです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x20**または .symopt 0x20、それぞれします。

このオプションは、DBH で既定でオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt +20 または symopt、-20 をそれぞれ使用します。

### <a name="span-idsymopt-load-anythingspanspan-idsymopt_load_anythingspansymopt_load_anything"></a><span id="symopt-load-anything"></span><span id="SYMOPT_LOAD_ANYTHING"></span>SYMOPT\_ロード\_すべて

このシンボルのオプションでは、シンボルと一致する際に、シンボル ハンドラーの pickiness が減少します。

このオプションは既定ではすべてのデバッガーではオフです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x40**または .symopt 0x40、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +40 または symopt-40, をそれぞれ使用します。

### <a name="span-idsymopt-ignore-cvrecspanspan-idsymopt_ignore_cvrecspansymopt_ignore_cvrec"></a><span id="symopt-ignore-cvrec"></span><span id="SYMOPT_IGNORE_CVREC"></span>SYMOPT\_無視\_CVREC

このシンボルのオプションではシンボルを検索するときに読み込まれたイメージ ヘッダーの CV レコードを無視するシンボル ハンドラー。

このオプションは既定ではすべてのデバッガーではオフです。 これは、-sicv コマンド ライン オプションを使用してアクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x80**または .symopt 0x80、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt+80 または symopt-80 をそれぞれ使用します。

### <a name="span-idsymopt-no-unqualified-loadsspanspan-idsymopt_no_unqualified_loadsspansymopt_no_unqualified_loads"></a><span id="symopt-no-unqualified-loads"></span><span id="SYMOPT_NO_UNQUALIFIED_LOADS"></span>SYMOPT\_いいえ\_UNQUALIFIED\_読み込み

このシンボルのオプションには、モジュールのシンボル ハンドラーの自動読み込みが無効にします。 このオプションを設定すると、デバッガーがシンボルを照合しようとした場合、既に読み込まれているモジュールのみが検索されます。

このオプションは、シンボル名の入力ミスからの防御として使用できます。 通常、入力の間違いシンボルでは、デバッガーはすべてのアンロードのシンボル ファイルを検索中に一時停止が発生します。 このオプションは、アクティブと入力の間違いシンボルが読み込まれたモジュールでは見つかりませんが、検索は終了し。

このオプションは既定ではすべてのデバッガーではオフです。 これは、-snul コマンド ライン オプションを使用してアクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x100**または .symopt 0x100、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt+100 または symopt-100 をそれぞれ使用します。

### <a name="span-idsymopt-fail-critical-errorsspanspan-idsymopt_fail_critical_errorsspansymopt_fail_critical_errors"></a><span id="symopt-fail-critical-errors"></span><span id="SYMOPT_FAIL_CRITICAL_ERRORS"></span>SYMOPT\_失敗\_重大\_エラー

このシンボルのオプションは、抑制する ダイアログ ボックスをファイル アクセス エラーになります。

このオプションがオフの場合は、ダイアログ ボックスが表示されると、「準備ができていませんドライブ」などのファイル アクセス エラーがシンボルの読み込み中に発生したなります。 このオプションがオンの場合は、これらのボックスが抑制され、すべてのアクセス エラーが「失敗」の応答を受信します。

このオプションは、すべてのデバッガーで既定でオンです。 -Sdce コマンド ライン オプションを使用して、非アクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x200**または .symopt 0x200、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +200 または symopt -200 をそれぞれ使用します。

### <a name="span-idsymopt-exact-symbolsspanspan-idsymopt_exact_symbolsspansymopt_exact_symbols"></a><span id="symopt-exact-symbols"></span><span id="SYMOPT_EXACT_SYMBOLS"></span>SYMOPT\_EXACT\_シンボル

このシンボル オプションでは、すべてのシンボル ファイルの厳密な評価を実行するデバッガーをによりします。

このオプションがオンのときにシンボル ファイルとシンボル ハンドラーの期待もわずか不一致が無視するシンボルに発生します。

このオプションは既定ではすべてのデバッガーではオフです。 Ses-コマンド ライン オプションを使用して、それをアクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x400**または .symopt 0x400、それぞれします。

-Failinc コマンド ライン オプションもオン SYMOPT\_EXACT\_SYMBOLS。 さらに、ユーザー モードのミニダンプまたはカーネル モードのミニダンプをデバッグする場合 - failinc は、デバッガーからのイメージをマップすることはできませんのすべてのモジュールの読み込みできません。

このオプションは、DBH で既定でオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt +400 または symopt-400 をそれぞれ使用します。

### <a name="span-idsymopt-allow-absolute-symbolsspanspan-idsymopt_allow_absolute_symbolsspansymopt_allow_absolute_symbols"></a><span id="symopt-allow-absolute-symbols"></span><span id="SYMOPT_ALLOW_ABSOLUTE_SYMBOLS"></span>SYMOPT\_許可\_絶対\_シンボル

このシンボルのオプションでは、メモリ内の絶対アドレスに格納されているシンボルを読み取る DbgHelp をできます。 このオプションは、ほとんどの場合では必要ありません。

このオプションは既定ではすべてのデバッガーではオフです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x800**または .symopt 0x800、それぞれします。

このオプションは、DBH で既定でオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt 当社は 800 以上または symopt-800 をそれぞれ使用します。

### <a name="span-idsymopt-ignore-nt-sympathspanspan-idsymopt_ignore_nt_sympathspansymopt_ignore_nt_sympath"></a><span id="symopt-ignore-nt-sympath"></span><span id="SYMOPT_IGNORE_NT_SYMPATH"></span>SYMOPT\_無視\_NT\_SYMPATH

このシンボル オプションを指定、デバッガーのシンボル パスと、実行可能イメージ パス環境変数の設定を無視するとします。

このオプションは既定ではすべてのデバッガーではオフです。 これは、-sins コマンド ライン オプションを使用してアクティブにできます。 ただし、制御することはできません **.symopt**起動時に環境変数は読み取りのみであるため、デバッガーが実行されるとします。

このオプションは、DBH で既定でオフは、すべてのケースで DBH は無視されます。

### <a name="span-idsymopt-publics-onlyspanspan-idsymopt_publics_onlyspansymopt_publics_only"></a><span id="symopt-publics-only"></span><span id="SYMOPT_PUBLICS_ONLY"></span>SYMOPT\_PUBLICS\_のみ

このシンボルのオプションでは DbgHelp プライベート シンボルのデータを無視して、シンボル情報をパブリック シンボル テーブルのみを検索します。 これは、動作をエミュレートします DbgHelp のサポートする前にこれらの型が追加されました。 [パブリック シンボルとプライベート シンボル](public-and-private-symbols.md)参照してください。

このオプションは既定ではすべてのデバッガーではオフです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x4000**または .symopt 0x4000、それぞれします。

このオプションは、既定で DBH でオフにします。 -D コマンド ライン オプションを使用する場合にオンです。 DBH が実行されていることができますにすることオンまたはオフ symopt +4000 または symopt-4000 をそれぞれ使用します。

### <a name="span-idsymopt-no-publicsspanspan-idsymopt_no_publicsspansymopt_no_publics"></a><span id="symopt-no-publics"></span><span id="SYMOPT_NO_PUBLICS"></span>SYMOPT\_いいえ\_PUBLICS

このシンボルのオプションでは、DbgHelp がパブリック シンボル テーブルを検索できなくなります。 これにより、symbol 列挙型、シンボルの検索がはるかに高速です。 検索の速度、SYMOPT のみに関係するかどうかは\_自動\_PUBLICS オプションはこのことをお勧めします。 パブリック シンボル テーブルについては、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

このオプションは既定ではすべてのデバッガーではオフです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x8000**または .symopt 0x8000、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +8000 または symopt-8000 をそれぞれ使用します。

### <a name="span-idsymopt-auto-publicsspanspan-idsymopt-auto-publicsspansymopt_auto_publics"></a><span id="symopt-auto-publics"></span><span id="SYMOPT-AUTO-PUBLICS"></span>SYMOPT\_自動\_PUBLICS

このシンボルのオプションは、最後の手段としての .pdb ファイルに、パブリック シンボル テーブルを検索する DbgHelp とします。 プライベート シンボル データを検索するときに、一致が見つかった場合、パブリック シンボルは検索されません。 これにより、シンボルの検索の速度が向上します。

このオプションは、すべてのデバッガーで既定でオンです。 使用して非アクティブ化することができます、sup コマンド ライン オプション。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x10000**または .symopt 0x10000、それぞれします。

このオプションは、DBH で既定でオンです。 電源オフ、-d コマンド ライン オプションを使用する場合。 DBH が実行されていることができますにすることオンまたはオフ symopt +10000 または symopt-10000 をそれぞれ使用します。

### <a name="span-idsymopt-no-image-searchspanspan-idsymopt-no-image-searchspansymopt_no_image_search"></a><span id="symopt-no-image-search"></span><span id="SYMOPT-NO-IMAGE-SEARCH"></span>SYMOPT\_いいえ\_イメージ\_検索

このシンボルのオプションでは、DbgHelp がシンボルが読み込まれるときに、ディスク上のイメージのコピーを検索できなくなります。

このオプションは、すべてのデバッガーで既定でオンです。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x20000**または .symopt 0x20000、それぞれします。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +20000 または symopt-20000 をそれぞれ使用します。

### <a name="span-idsymopt-securespanspan-idsymopt_securespansymopt_secure"></a><span id="symopt-secure"></span><span id="SYMOPT_SECURE"></span>SYMOPT\_SECURE

(カーネル モードのみ)このシンボル オプションを指定するかどうか[保護モード](secure-mode.md)がアクティブです。

セキュリティで保護されたモードは、既定ですべてのデバッガーでオフです。 使用してアクティブ化は、セキュリティで保護されたコマンド ライン オプション。 使用してセキュリティで保護モードをオンにできる場合、デバッガーが実行されている、休止モードでは、デバッグ サーバーが確立されていないが、 **.symopt + 0x40000**または[ **.secure (セキュリティで保護モードをアクティブ化)** ](-secure--activate-secure-mode-.md).

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +40000 または symopt-40000 をそれぞれ使用します。

アクティブ化すると、セキュリティで保護されたモードをオフにしないことができます。

### <a name="span-idsymopt-no-promptsspanspan-idsymopt_no_promptsspansymopt_no_prompts"></a><span id="symopt-no-prompts"></span><span id="SYMOPT_NO_PROMPTS"></span>SYMOPT\_NO\_PROMPTS

このシンボルのオプションは、プロキシ サーバーからの認証ダイアログ ボックスを表示しません。 これにより、SymSrv がインターネット上のシンボル ストアにアクセスできない可能性があります。

詳細については、次を参照してください。[ファイアウォールとプロキシ サーバー](firewalls-and-proxy-servers.md)します。

KD、CDB でこのオプションが既定でオンです。WinDbg では、このオプションは、既定でオフは。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x80000**または .symopt 0x80000 はそれぞれ、後ろ、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。 これは、ことができますにすることもオンとオフを使用して、 [ **! オフ sym が求められます**](-sym.md)と **! sym メッセージが表示されます**拡張機能のコマンドを続けて、 **.reload (モジュール)** コマンド。

このオプションは、既定で DBH でオフにします。 DBH が実行されていることができますにすることオンまたはオフ symopt +80000 または symopt-80000 をそれぞれ使用します。

### <span id="symopt-disable-fast-symbols"></span>

### <span id="symopt_disable_symsrv_timeout"></span>

### <a name="span-idsymopt-debugspan-symopt_debug"></a><span id="symopt-debug"></span>-SYMOPT\_デバッグ

このシンボル オプションをオンに*ノイズの多いシンボルの読み込み*します。 これには、デバッガーのシンボルの検索についての情報を表示するように指示します。

読み込まれると、各シンボル ファイルの名前が表示されます。 デバッガーがシンボル ファイルを読み込むことはできませんがある場合、エラー メッセージが表示されます。 .Pdb ファイルのエラー メッセージがテキストで表示されます。 .Dbg ファイルのエラー メッセージがエラー コード; の形式になりますこれらのコードは、winerror.h ファイルについて説明します。

シンボル ヘッダー情報を回復するためだけにイメージ ファイルが読み込まれる場合もこの表示されます。

このオプションは既定ではすべてのデバッガーではオフです。 これは、-n コマンド ライン オプションを使用してアクティブにできます。 デバッガーが実行されていることができますにすることオンまたはオフを使用して **.symopt + 0x80000000**または .symopt 0x80000000、それぞれします。 これにすることもオンとオフを使用して、 [ **! sym ノイズの多い**](-sym.md)と **! sym quiet**拡張コマンド。

**注**  ノイズの多いと、このオプションを混同しない必要があります*ソース*--読み込みによって制御される、 [ **.srcnoisy (Noisy Source Loading)** ](-srcnoisy--noisy-source-loading-.md)コマンド。

 

このオプションは、既定で DBH でオフにします。 これは、-n コマンド ライン オプションを使用してアクティブにできます。 DBH が実行されていることができますにすることオンまたはオフ symopt +80000000 または symopt-80000000 をそれぞれ使用します。 これは、ことができますにすることもオンとオフの詳細およびコマンドの詳細を使用しています。

 

 





