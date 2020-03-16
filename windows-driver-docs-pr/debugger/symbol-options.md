---
title: シンボルのオプション
description: シンボルのオプション
ms.assetid: 4a501ea3-431c-4c11-8826-154eb8799a64
keywords:
- シンボル、設定 (シンボルオプションを)
- シンボル、SYMOPT_XXXX
- ノイズの多いシンボルの読み込み
- CV レコード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9832b751affe05bd31977c0a82280a3e2f692e7b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242787"
---
# <a name="symbol-options"></a>シンボルのオプション


## <span id="ddk_setting_symbol_options_dbg"></span><span id="DDK_SETTING_SYMBOL_OPTIONS_DBG"></span>


シンボルの読み込みと使用方法を制御するためのオプションが多数用意されています。 これらのオプションは、さまざまな方法で設定できます。

次の表に、これらのシンボルオプションの一覧を示します。

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
<th align="left">デバッガーでの既定値</th>
<th align="left">DBH の既定値</th>
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
<td align="left"><p>KD と CDB での無効化</p>
<p>WinDbg での</p></td>
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
<td align="left"><p>0x80000</p></td>
<td align="left"><p><a href="#symopt-no-prompts" data-raw-source="[SYMOPT_NO_PROMPTS](#symopt-no-prompts)">SYMOPT_NO_PROMPTS</a></p></td>
<td align="left"><p>KD と CDB での</p>
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

 

### <a name="span-idchanging-the-symbol-option-settingsspanspan-idchanging_the_symbol_option_settingsspanchanging-the-symbol-option-settings"></a><span id="changing-the-symbol-option-settings"></span><span id="CHANGING_THE_SYMBOL_OPTION_SETTINGS"></span>シンボルオプションの設定の変更

[シンボルオプションの[**設定**](-symopt--set-symbol-options-.md)] コマンドを使用すると、シンボルオプションの設定を変更または表示できます。 また、これらの設定を変更するために、多数のコマンドラインパラメーターとコマンドを使用できます。これらは、個々の SYMOPT\_*XXX*セクションに記載されています。

**-Sflags**[コマンドラインオプション](command-line-options.md)を使用して、一度にすべての設定を制御することもできます。 このオプションの後には、10進数、または**0x**で始まる16進数の数字を使用できます。 シンボルフラグが適切にアラインされているため、16進数を使用することをお勧めします。 このメソッドは、ビットフィールド全体を設定し、すべてのシンボルハンドラーの既定値をオーバーライドするため、慎重に使用してください。 たとえば、 **-sflags 0x401**は symopt\_正確に\_シンボルと symopt\_大文字\_小文字を区別しないようにしますが、既定では、通常はオンになっている他のすべてのオプションも無効になります。

合計フラグビットの既定値は、WinDbg では0x30237、CDB と KD では0xB0227、 [DBH ツール](dbh.md)では0x10C13 で、シンボル関連のコマンドラインオプションを指定せずにこれらのプログラムが起動されます。

### <a name="span-idsymopt-case-insensitivespanspan-idsymopt_case_insensitivespansymopt_case_insensitive"></a><span id="symopt-case-insensitive"></span><span id="SYMOPT_CASE_INSENSITIVE"></span>SYMOPT\_CASE\_INSENSITIVE

このシンボルオプションを使用すると、シンボル名のすべての検索で大文字と小文字が区別されません。

このオプションは、すべてのデバッガーで既定でオンになっています。 デバッガーが実行されたら、 **symopt + 0x1**または symopt-0x1 をそれぞれ使用して、有効または無効にすることができます。

このオプションは、DBH では既定でオンになっています。 DBH を実行すると、symopt + 1 または symopt-1 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-undnamespanspan-idsymopt_undnamespansymopt_undname"></a><span id="symopt-undname"></span><span id="SYMOPT_UNDNAME"></span>SYMOPT\_UNDNAME

このシンボルオプションを使用すると、パブリックシンボル名が表示されるときに非装飾になり、シンボル名を検索するとシンボルの装飾が無視されます。 このオプションがアクティブかどうかにかかわらず、プライベートシンボル名は修飾されません。 シンボル名の装飾の詳細については、「[パブリックシンボルとプライベートシンボル](public-and-private-symbols.md)」を参照してください。

このオプションは、すべてのデバッガーで既定でオンになっています。 デバッガーが実行されると、それぞれ**symopt + 0x2**または symopt-0x2 を使用して、有効または無効にすることができます。

このオプションは、DBH では既定でオンになっています。 -D コマンドラインオプションが使用されている場合、このオプションはオフになっています。 DBH を実行すると、symopt + 2 または symopt-2 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-deferred-loadsspanspan-idsymopt_deferred_loadsspansymopt_deferred_loads"></a><span id="symopt-deferred-loads"></span><span id="SYMOPT_DEFERRED_LOADS"></span>SYMOPT\_遅延\_読み込み

このシンボルオプションは、*遅延シンボルの読み込み*または*遅延シンボルの読み込み*と呼ばれます。 アクティブになっている場合、ターゲットモジュールが読み込まれるときにシンボルは実際には読み込まれません。 代わりに、必要に応じてシンボルがデバッガーによって読み込まれます。 詳細については、「[遅延シンボルの読み込み](deferred-symbol-loading.md)」を参照してください。

このオプションは、すべてのデバッガーで既定でオンになっています。 CDB および KD では、-s コマンドラインオプションを指定すると、このオプションはオフになります。 また、[ツール .ini](configuring-tools-ini.md)ファイルの**lazyload**変数を使用して、CDB で無効にすることもできます。 デバッガーが実行されたら、このオプションを有効または無効にするには、それぞれ**symopt + 0x4**または. symopt-0x4 を使用します。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 4 または symopt-4 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-no-cppspanspan-idsymopt_no_cppspansymopt_no_cpp"></a><span id="symopt-no-cpp"></span><span id="SYMOPT_NO_CPP"></span>SYMOPT\_\_CPP

このシンボルオプションは、 C++翻訳をオフにします。 この記号オプションが設定されている場合、 **::** は、すべての記号で **\_\_** に置き換えられます。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-snc コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行されたら、 **symopt + 0x8**または symopt-0x8 をそれぞれ使用して、有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH の実行が完了すると、symopt + 8 または symopt-8 を使用して有効または無効にすることができます。

### <a name="span-idsymopt-load-linesspanspan-idsymopt_load_linesspansymopt_load_lines"></a><span id="symopt-load-lines"></span><span id="SYMOPT_LOAD_LINES"></span>SYMOPT\_読み込み\_の行

このシンボルオプションを使用すると、ソースファイルから行番号の情報を読み取ることができます。 ソースデバッグが正常に機能するためには、このオプションがオンになっている必要があります。

KD および CDB では、このオプションは既定でオフになっています。WinDbg では、このオプションは既定でオンになっています。 CDB および KD では、-lines コマンドラインオプションによってこのオプションが有効になります。 デバッガーが実行されたら、 **symopt + 0x10**または symopt-0x10 を使用して有効または無効にすることができます。 また、 [ **. lines (ソースラインサポートの切り替え)** ](-lines--toggle-source-line-support-.md)コマンドを使用して、オンとオフを切り替えることもできます。

このオプションは、DBH では既定でオンになっています。 DBH の実行が完了すると、symopt + 10 または symopt-10 を使用して有効または無効にすることができます。

### <a name="span-idsymopt-omap-find-nearestspanspan-idsymopt_omap_find_nearestspansymopt_omap_find_nearest"></a><span id="symopt-omap-find-nearest"></span><span id="SYMOPT_OMAP_FIND_NEAREST"></span>SYMOPT\_OMAP\_最も近い\_を検索します

コードが最適化されていて、必要な位置にシンボルがない場合、このオプションを使用すると、最も近いシンボルが代わりに使用されます。

このオプションは、すべてのデバッガーで既定でオンになっています。 デバッガーが実行されると、それぞれ**symopt + 0x20**または. symopt-0x20 を使用して有効または無効にすることができます。

このオプションは、DBH では既定でオンになっています。 DBH を実行すると、symopt + 20 または symopt-20 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-load-anythingspanspan-idsymopt_load_anythingspansymopt_load_anything"></a><span id="symopt-load-anything"></span><span id="SYMOPT_LOAD_ANYTHING"></span>SYMOPT\_読み込み\_任意

このシンボルオプションを指定すると、シンボルを照合しようとしたときのシンボルハンドラーの pickiness が減少します。

このオプションは、すべてのデバッガーで既定でオフになっています。 デバッガーが実行されたら、 **symopt + 0x40**または symopt-0x40 をそれぞれ使用して、有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 40 または symopt-40 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-ignore-cvrecspanspan-idsymopt_ignore_cvrecspansymopt_ignore_cvrec"></a><span id="symopt-ignore-cvrec"></span><span id="SYMOPT_IGNORE_CVREC"></span>SYMOPT\_\_CVREC を無視する

シンボルを検索するときに、シンボルハンドラーによって読み込まれたイメージヘッダーの CV レコードが無視されます。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-sicv コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行されると、それぞれ**symopt + 0x80**または symopt-0x80 を使用して有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 80 または symopt-80 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-no-unqualified-loadsspanspan-idsymopt_no_unqualified_loadsspansymopt_no_unqualified_loads"></a><span id="symopt-no-unqualified-loads"></span><span id="SYMOPT_NO_UNQUALIFIED_LOADS"></span>SYMOPT\_\_非修飾\_読み込み

このシンボルオプションは、シンボルハンドラーによるモジュールの自動読み込みを無効にします。 このオプションを設定し、デバッガーがシンボルとの照合を試みると、既に読み込まれているモジュールだけが検索されます。

このオプションは、シンボル名の形式を設定するための防御として使用できます。 通常、入力ミスのシンボルを入力すると、アンロードされたすべてのシンボルファイルの検索中にデバッガーが一時停止します。 このオプションがアクティブになっている場合は、読み込まれたモジュールに入力ミスのシンボルが見つからないため、検索が終了します。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-snul コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行されると、それぞれ**symopt + 0x100**または symopt-0x100 を使用して有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 100 または symopt-100 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-fail-critical-errorsspanspan-idsymopt_fail_critical_errorsspansymopt_fail_critical_errors"></a><span id="symopt-fail-critical-errors"></span><span id="SYMOPT_FAIL_CRITICAL_ERRORS"></span>SYMOPT\_失敗\_重大\_エラー

このシンボルオプションを使用すると、ファイルアクセスエラーのダイアログボックスが表示されなくなります。

このオプションがオフの場合、シンボルの読み込み中に "ドライブが準備できていません" などのファイルアクセスエラーが発生すると、ダイアログボックスが表示されます。 このオプションがオンの場合、これらのボックスは表示されず、すべてのアクセスエラーは "fail" 応答を受け取ります。

このオプションは、すべてのデバッガーで既定でオンになっています。 -Sdce コマンドラインオプションを使用して非アクティブにすることができます。 デバッガーが実行されると、それぞれ**symopt + 0x200**または symopt-0x200 を使用して、有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 200 または symopt-200 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-exact-symbolsspanspan-idsymopt_exact_symbolsspansymopt_exact_symbols"></a><span id="symopt-exact-symbols"></span><span id="SYMOPT_EXACT_SYMBOLS"></span>SYMOPT\_正確な\_シンボル

このシンボルオプションを指定すると、デバッガーはすべてのシンボルファイルの厳密な評価を実行します。

このオプションがオンになっている場合、シンボルファイルとシンボルハンドラーの期待のほとんどが一致しなくても、シンボルは無視されます。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-ses コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行されたら、 **symopt + 0x400**または symopt-0x400 をそれぞれ使用して、有効または無効にすることができます。

-Failinc コマンドラインオプションを指定すると、SYMOPT\_正確に\_記号も有効になります。 さらに、ユーザーモードミニダンプまたはカーネルモードミニダンプをデバッグしている場合は、-failinc によって、イメージをマップできないモジュールをデバッガーで読み込むことができなくなります。

このオプションは、DBH では既定でオンになっています。 DBH を実行すると、symopt + 400 または symopt-400 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-allow-absolute-symbolsspanspan-idsymopt_allow_absolute_symbolsspansymopt_allow_absolute_symbols"></a><span id="symopt-allow-absolute-symbols"></span><span id="SYMOPT_ALLOW_ABSOLUTE_SYMBOLS"></span>SYMOPT\_\_絶対\_シンボルを許可します

このシンボルオプションを使用すると、メモリ内の絶対アドレスに格納されているシンボルを DbgHelp で読み取ることができます。 ほとんどの場合、このオプションは必要ありません。

このオプションは、すべてのデバッガーで既定でオフになっています。 デバッガーが実行されると、それぞれ**symopt + 0x800**または symopt-0x800 を使用して有効または無効にすることができます。

このオプションは、DBH では既定でオンになっています。 DBH を実行すると、symopt + 800 または symopt-800 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-ignore-nt-sympathspanspan-idsymopt_ignore_nt_sympathspansymopt_ignore_nt_sympath"></a><span id="symopt-ignore-nt-sympath"></span><span id="SYMOPT_IGNORE_NT_SYMPATH"></span>SYMOPT\_\_NT\_SYMPATH を無視します

このシンボルオプションを使用すると、シンボルパスと実行可能イメージパスの環境変数の設定がデバッガーによって無視されます。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-sins コマンドラインオプションを使用してアクティブにすることができます。 ただし、環境変数は起動時にのみ読み込まれるため、デバッガーの実行後に**symopt**で制御することはできません。

このオプションは DBH では既定でオフになっており、すべての場合に DBH によって無視されます。

### <a name="span-idsymopt-publics-onlyspanspan-idsymopt_publics_onlyspansymopt_publics_only"></a><span id="symopt-publics-only"></span><span id="SYMOPT_PUBLICS_ONLY"></span>SYMOPT\_PUBLICS\_のみ

このシンボルオプションでは、DbgHelp によってプライベートシンボルデータが無視され、シンボル情報についてはパブリックシンボルテーブルだけが検索されます。 これは、これらの種類のサポートが追加される前に、DbgHelp の動作をエミュレートします。 「[パブリックシンボルとプライベートシンボル」を](public-and-private-symbols.md)参照してください。

このオプションは、すべてのデバッガーで既定でオフになっています。 デバッガーが実行されると、それぞれ**symopt + 0x4000**または symopt-0x4000 を使用して有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 -D コマンドラインオプションを使用すると、有効になります。 DBH を実行すると、symopt + 4000 または symopt-4000 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-no-publicsspanspan-idsymopt_no_publicsspansymopt_no_publics"></a><span id="symopt-no-publics"></span><span id="SYMOPT_NO_PUBLICS"></span>SYMOPT\_NO\_PUBLICS

このシンボルオプションは、DbgHelp がパブリックシンボルテーブルを検索できないようにします。 これにより、シンボルの列挙やシンボル検索をはるかに高速に行うことができます。 検索速度だけを考慮する場合は、通常、SYMOPT\_AUTO\_PUBLICS オプションを使用することをお勧めします。 パブリックシンボルテーブルの詳細については、「[パブリックシンボルとプライベートシンボル](public-and-private-symbols.md)」を参照してください。

このオプションは、すべてのデバッガーで既定でオフになっています。 デバッガーが実行されたら、 **symopt + 0x8000**または symopt-0x8000 をそれぞれ使用して、有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 8000 または symopt-8000 をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-auto-publicsspanspan-idsymopt-auto-publicsspansymopt_auto_publics"></a><span id="symopt-auto-publics"></span><span id="SYMOPT-AUTO-PUBLICS"></span>SYMOPT\_AUTO\_PUBLICS

このシンボルオプションを使用すると、最新の手段としてのみ .pdb ファイル内のパブリックシンボルテーブルを検索できます。 プライベートシンボルデータの検索時に一致するものが見つかった場合、パブリックシンボルは検索されません。 これにより、シンボル検索速度が向上します。

このオプションは、すべてのデバッガーで既定でオンになっています。 -Sup コマンドラインオプションを使用して非アクティブにすることができます。 デバッガーが実行されると、それぞれ**symopt +** を使用して有効または無効にすることができます。

このオプションは、DBH では既定でオンになっています。 -D コマンドラインオプションが使用されている場合、このオプションはオフになっています。 DBH を実行すると、symopt + 1万または symopt-1万をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-no-image-searchspanspan-idsymopt-no-image-searchspansymopt_no_image_search"></a><span id="symopt-no-image-search"></span><span id="SYMOPT-NO-IMAGE-SEARCH"></span>SYMOPT\_\_イメージ\_検索

このシンボルオプションを使用すると、シンボルが読み込まれたときに、DbgHelp がイメージのコピーをディスクから検索できなくなります。

このオプションは、すべてのデバッガーで既定でオンになっています。 デバッガーが実行されると、それぞれ**symopt + 0x20000**または0x20000 を使用して、有効または無効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 2万または symopt-2万をそれぞれ使用して、有効または無効にすることができます。

### <a name="span-idsymopt-securespanspan-idsymopt_securespansymopt_secure"></a><span id="symopt-secure"></span><span id="SYMOPT_SECURE"></span>SYMOPT\_セキュリティ保護されています

(カーネルモードのみ)このシンボルオプションは、[保護モード](secure-mode.md)がアクティブであるかどうかを示します。

既定では、すべてのデバッガーで保護モードがオフになっています。 これは、-secure コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行中で、が休止モードであり、デバッグサーバーが確立されていない場合は、 **. symopt + 0x40000**または[**Secure (保護モードのアクティブ化)** ](-secure--activate-secure-mode-.md)を使用して、保護モードを有効にすることができます。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 4万または symopt-4万をそれぞれ使用して、有効または無効にすることができます。

保護モードがアクティブになった後は、保護モードをオフにすることはできません。

### <a name="span-idsymopt-no-promptsspanspan-idsymopt_no_promptsspansymopt_no_prompts"></a><span id="symopt-no-prompts"></span><span id="SYMOPT_NO_PROMPTS"></span>SYMOPT\_\_プロンプトが表示されない

この記号オプションを指定すると、プロキシサーバーからの認証ダイアログボックスが表示されなくなります。 これにより、SymSrv がインターネット上のシンボルストアにアクセスできなくなる可能性があります。

詳細については、「[ファイアウォールとプロキシサーバー](firewalls-and-proxy-servers.md)」を参照してください。

KD および CDB では、このオプションは既定でオンになっています。WinDbg では、このオプションは既定でオフになっています。 デバッガーが実行されたら、次に、それぞれ**symopt + 0x80000**または symopt-0x80000 を使用し、その後に[**再読み込み (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンドを実行します。 また、 [ **! sym プロンプト**](-sym.md)と **! sym**プロンプトを使用して有効または無効にすることもできます。この場合は、拡張子コマンドの後に、**再読み込み (モジュールの再読み込み)** コマンドを実行します。

DBH では、このオプションは既定でオフになっています。 DBH を実行すると、symopt + 8万または symopt-8万をそれぞれ使用して、有効または無効にすることができます。

### <span id="symopt-disable-fast-symbols"></span>

### <span id="symopt_disable_symsrv_timeout"></span>

### <a name="span-idsymopt-debugspan-symopt_debug"></a><span id="symopt-debug"></span>-SYMOPT\_デバッグ

このシンボルオプションは、*ノイズ*の多いシンボルの読み込みを有効にします。 これは、シンボルの検索に関する情報を表示するようにデバッガーに指示します。

各シンボルファイルの名前は、読み込まれたときに表示されます。 デバッガーがシンボルファイルを読み込むことができない場合は、エラーメッセージが表示されます。 .Pdb ファイルのエラーメッセージがテキストで表示されます。 Dbg ファイルのエラーメッセージは、エラーコードの形式で表示されます。これらのコードについては、winerror.h ファイルをご説明します。

シンボルヘッダー情報を回復するためだけにイメージファイルが読み込まれる場合は、これも表示されます。

このオプションは、すべてのデバッガーで既定でオフになっています。 これは、-n コマンドラインオプションを使用してアクティブにすることができます。 デバッガーが実行されると、それぞれ**symopt + 0x80000000**または symopt-0x80000000 を使用して、デバッガーを有効または無効にすることができます。 また、 [ **! sym の雑音**](-sym.md)と **! sym quiet**拡張コマンドを使用して、有効または無効にすることもできます。

**注**   このオプションは、非常に複雑な[ **(ノイズのあるソースの読み込み)** ](-srcnoisy--noisy-source-loading-.md)コマンドによって制御される、ノイズのある*ソース*の読み込みと混同しないようにしてください。

 

DBH では、このオプションは既定でオフになっています。 これは、-n コマンドラインオプションを使用してアクティブにすることができます。 DBH を実行すると、symopt + 8000万または symopt-8000万をそれぞれ使用して、有効または無効にすることができます。 また、verbose on および verbose off コマンドを使用して、有効または無効にすることもできます。

 

 





