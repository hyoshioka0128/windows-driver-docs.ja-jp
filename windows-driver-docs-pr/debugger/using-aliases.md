---
title: エイリアスの使用
description: エイリアスの使用
ms.assetid: ee0540d0-5bfd-47ef-92b1-ec1d6954aec7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ccd9591a1dae66008545a28b85ea37407440f6a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349767"
---
# <a name="using-aliases"></a>エイリアスの使用


## <span id="ddk_using_aliases_dbg"></span><span id="DDK_USING_ALIASES_DBG"></span>


*エイリアス*文字の文字列は、その他の文字の文字列に自動的に置き換えられますです。 デバッガーのコマンドで、特定の一般的なフレーズを再入力を回避するために使用できます。

エイリアスから成る、*エイリアス名*と*エイリアスと同等*します。 デバッガー コマンドの一部として、エイリアス名を使用すると、名前はエイリアスと同等に自動的に置換されます。 この置換は、コマンドが解析または実行される前に、すぐに行われます。

デバッガーには、エイリアスの 3 種類がサポートされています。

-   名前を設定することができます*という名前のユーザーのエイリアス*します。

-   設定することができます*固定名のエイリアス*、という名前が**ドル u0**、 **$u1**,...,**ドル u9**します。

-   デバッガーを設定し、名前*自動エイリアス*します。

### <a name="span-iddefiningausernamedaliasspanspan-iddefiningausernamedaliasspandefining-a-user-named-alias"></a><span id="defining_a_user_named_alias"></span><span id="DEFINING_A_USER_NAMED_ALIAS"></span>という名前のユーザーのエイリアスを定義します。

という名前のユーザーのエイリアスを定義するときに、エイリアス名とエイリアス相当するものを選択できます。

-   エイリアス名には、空白文字を含まない任意の文字列を指定できます。

-   エイリアスと同等では、任意の文字列を指定できます。 場合は、キーボードで入力すると、エイリアスと同等は先頭のスペースまたはキャリッジ リターンを含めることはできません。 または、ことで設定する文字列と等しいメモリ、ファイル、環境変数の値または 1 つまたは複数のデバッガー コマンドの出力の内容、数値式の値。

エイリアス名とエイリアスと同等の両方が、大文字小文字を区別します。

または、という名前のユーザーのエイリアスを再定義するを使用して、 [ **(設定の別名) として**](as--as--set-alias-.md)または **(設定の別名) として**コマンド。

エイリアスを削除するには、使用、 [ **ad (エイリアスの削除)** ](ad--delete-alias-.md)コマンド。

現在のユーザーというエイリアスを一覧表示する、 [ **al (一覧のエイリアス)** ](al--list-aliases-.md)コマンド。

### <a name="span-iddefiningafixednamealiasspanspan-iddefiningafixednamealiasspandefining-a-fixed-name-alias"></a><span id="defining_a_fixed_name_alias"></span><span id="DEFINING_A_FIXED_NAME_ALIAS"></span>固定名のエイリアスを定義します。

10 個の固定名のエイリアスがあります。 エイリアス名は**ドル u0**、 **$u1**,...,**ドル u9**します。 同等のエイリアスには、ENTER キーを含まない任意の文字列を指定できます。

使用して、 [ **r (レジスタ)** ](r--registers-.md)エイリアスと同等の固定名のエイリアスを定義するコマンド。 固定名のエイリアスを定義するときに、ピリオドを挿入する必要があります (**.**) 文字"u"の前にします。 等号 (=) が、エイリアスの後のテキストと同じです。 エイリアスに相当はスペースまたはセミコロンを含めることができますが、先頭と末尾のスペースは無視されます。 、(引用符を含む結果をしない) 場合、エイリアスと同等を引用符で囲む必要があります。

**注**  は混同しないを使用して、 **r (レジスタ)** 固定名のエイリアス コマンド。 これらのエイリアスはいないレジスタと擬似レジスタを使用する場合でも、 **r**対応するエイリアスを設定するコマンド。 追加する必要はありませんで (**@**) サインインして、これらの別名が使用することはできません前に、 **r**コマンドを*表示*これらの別名のいずれかの値。

 

既定では、固定名のエイリアスを定義していない場合、空の文字列は。

### <a name="span-idautomaticaliasesspanspan-idautomaticaliasesspanautomatic-aliases"></a><span id="automatic_aliases"></span><span id="AUTOMATIC_ALIASES"></span>自動のエイリアス

デバッガーでは、次の自動のエイリアスを設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エイリアス名</th>
<th align="left">エイリアスと同等</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$ntnsym</strong></p></td>
<td align="left"><p>NT シンボルをコンピューターのネイティブ アーキテクチャ上の最も適切なモジュール。 このエイリアスがいずれかに等しい<strong>ntdll</strong>または<strong>nt</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ntwsym</strong></p></td>
<td align="left"><p>NT シンボルを 32 ビットのデバッグ中の最も適切なモジュールでは、WOW64 を使用します。 このエイリアスにすることが<strong>ntdll32</strong> Ntdll.dll の他のいくつかの 32 ビット バージョン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ntsym</strong></p></td>
<td align="left"><p>NT シンボルを現在のコンピューター モードに一致するための最も適切なモジュール。 このエイリアスが同じではネイティブ モードでデバッグするときに<strong>$ntnsym</strong>します。 非ネイティブ モードでデバッグするとき、デバッガーは、このモードと一致するモジュールを検索しようとします。 (たとえば、32 ビットは、WOW64 を使用するデバッグ、中にこのエイリアスは、同じとして<strong>$ntwsym</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpFile</strong></p></td>
<td align="left"><p>デバッガーが読み込まれている最後のダンプ ファイルの名前。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpPath</strong></p></td>
<td align="left"><p>デバッガーが読み込まれている最後のダンプ ファイルのディレクトリ パス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$CurrentDumpArchiveFile</strong></p></td>
<td align="left"><p>最後のダンプ アーカイブ ファイル (CAB ファイル)、デバッガーが読み込まれているの名前。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$CurrentDumpArchivePath</strong></p></td>
<td align="left"><p>最後のダンプ アーカイブ ファイル (CAB ファイルの)、デバッガーが読み込まれているディレクトリのパス。</p></td>
</tr>
</tbody>
</table>

 

自動のエイリアスはのような[自動の擬似レジスタ](pseudo-register-syntax.md)エイリアスに関連するトークンを使用した自動エイリアスを使用することを除いて、(など **$ {}**)、これらの擬似レジスタを使用することはできませんトークンです。

### <a name="span-idusinganaliasinthedebuggercommandwindowspanspan-idusinganaliasinthedebuggercommandwindowspanusing-an-alias-in-the-debugger-command-window"></a><span id="using_an_alias_in_the_debugger_command_window"></span><span id="USING_AN_ALIAS_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウで、別名を使用

エイリアスを定義した後は、任意のコマンドのエントリで使用することができます。 エイリアス名はエイリアスと等価に自動的に置き換えられます。 そのため、式として、またはマクロのエイリアスを使用できます。

エイリアス名を引用符で囲まれている場合でも正しく展開します。 エイリアスと同等では、任意の数の引用符またはセミコロンを含めることができます、ため、エイリアスと同等では複数のコマンドを表すことができます。

という名前のユーザーのエイリアスが認識されるは、その名前が他の文字から空白で区切られた場合にのみです。 エイリアス名の最初の文字は、線の始点か、スペース、セミコロン、または二重引用符に従う必要があります。 エイリアス名の最後の文字は、行を終了する必要がありますか、スペース、セミコロン、または二重引用符、後にします。

**注**  に入力した任意のテキスト、[デバッガー コマンド ウィンドウ](debugger-command-window.md)"aS"、"ad"、"as"で始まるまたは"al"はエイリアスの置換を受信しません。 この制限は、エイリアス コマンドが動作不能と表示されていることを防ぎます。 ただし、この制限も意味続くコマンド**ad**または**al**行ではありません、別名が置き換えられます。 これらの文字列のいずれかで始まる行で置換する別名を設定する場合は、エイリアスの前にセミコロンを追加します。

 

ただし、使用することができます、 **$ {}** その他のテキストの横にある場合でも、という名前のユーザーのエイリアスを展開するためのトークン。 エイリアスが拡張されることを防ぐために、または特定のエイリアスに関連する値を表示する特定のスイッチと共にこのトークンを使用することもできます。 このような状況の詳細については、次を参照してください。 [ **$ {} (別名インタープリター)**](-------alias-interpreter-.md)します。

固定名のエイリアスは、行のテキスト内で埋め込む方法に関係なく、行内の任意の時点から正しく展開します。

WinDbg でのみ使用可能なコマンドを使用することはできません ([**.open**](-open--open-source-file-.md)、 [ **.write\_cmd\_hist (書き込みコマンドの履歴)** ](-write-cmd-hist--write-command-history-.md)、 [ **.lsrcpath**](-srcpath---lsrcpath--set-source-path-.md)、および[ **.lsrcfix**](-srcfix---lsrcfix--use-source-server-.md)) とその他のいくつかのコマンド ([***.hh***](-hh--open-html-help-file-.md)、 [ **.cls**](-cls--clear-screen-.md)、 [ **.wtitle**](-wtitle--set-window-title-.md)、 [**.remote**](-remote--create-remote-exe-server-.md)、カーネル モード[ **.restart**](-restart--restart-kernel-connection-.md)とユーザー モード[ **.restart** ](-restart--restart-target-application-.md))エイリアスを使用します。

### <a name="span-idusinganaliasinascriptfilespanspan-idusinganaliasinascriptfilespanusing-an-alias-in-a-script-file"></a><span id="using_an_alias_in_a_script_file"></span><span id="USING_AN_ALIAS_IN_A_SCRIPT_FILE"></span>スクリプト ファイルで別名を使用します。

スクリプト ファイルで別名を使用する場合は、適切な時にエイリアスが展開されているかどうかを確認する特別な注意を行う必要があります。 次のスクリプトを検討してください。

```text
.foreach (value {dd 610000 L4})
{
   as /x ${/v:myAlias} value + 1
   .echo value myAlias
}

ad myAlias
```

ループで初めて、 [**として (設定の別名) として**](as--as--set-alias-.md)コマンドは、myAlias に値を割り当てます。 MyAlias に割り当てられている値は、1 を足した 610000 (dd コマンドの最初の出力) です。 ただし、ときに、 [ **.echo (エコー コメント)** ](-echo--echo-comment-.md)コマンドが実行され、myAlias まだ拡張されていない、610001 ではなく、テキスト"myAlias"確認ためです。

```dbgcmd
0:001> $$>< c:\Script02.txt
00610000 myAlias
00905a4d 0x610001
00000003 0x905a4e
00000004 0x4
0000ffff 0x5
```

問題は、新しいコードのブロックが入力されるまで、その myAlias は展開されません。 ループには、次のエントリは、myAlias 610001 を展開するための新しいブロックです。 遅すぎて、: 見るべき 610001 2 番目の時間ではなく、ループの最初の時間。それを囲むによってこの問題を修正しました、 [ **.echo (エコー コメント)** ](-echo--echo-comment-.md)新しいブロックのコマンドは、次のスクリプトに示すようにします。

```text
.foreach (value {dd 610000 L4}) 
{
   as /x ${/v:myAlias} value + 1
   .block{.echo value myAlias}
}

ad myAlias
```

変更されたスクリプトでは、次の正しい出力を取得します。

```dbgcmd
0:001> $$>< c:\Script01.txt
00610000 0x610001
00905a4d 0x905a4e
00000003 0x4
00000004 0x5
0000ffff 0x10000
```

詳細については、次を参照してください。 [ **.block** ](-block.md)と[ **$ {} (別名インタープリター)**](-------alias-interpreter-.md)します。

### <a name="span-idusingaforeachtokeninanaliasspanspan-idusingaforeachtokeninanaliasspanspan-idusingaforeachtokeninanaliasspanusing-a-foreach-token-in-an-alias"></a><span id="Using_a_.foreach_Token_in_an_Alias"></span><span id="using_a_.foreach_token_in_an_alias"></span><span id="USING_A_.FOREACH_TOKEN_IN_AN_ALIAS"></span>エイリアスに .foreach トークンを使用します。

使用すると、 [ **.foreach** ](-foreach.md)エイリアスの定義でトークンを行う必要があります、トークンが展開されていることを確認するには特別な注意します。 次のコマンド シーケンスを検討してください。

```dbgcmd
r $t0 = 5
ad myAlias
.foreach /pS 2 /ps 2 (Token {?@$t0}) {as myAlias Token}
al
```

最初のコマンドの値の設定、 **$t0**擬似レジスタを 5 にします。 2 番目のコマンドでは、任意の値が以前に割り当てられている myAlias を削除します。 3 番目のコマンドは、3 つ目はのトークン、 **? @$ t0**コマンドと myAlias にそのトークンの値を割り当てようとするとします。 4 番目のコマンドは、すべてのエイリアスとその値を一覧表示します。 5 個、myAlias の値を予想はなく、値「トークン」という単語です。

```dbgcmd
   Alias            Value  
 -------          ------- 
 myAlias          Token 
```

問題なは、 [**として**](as--as--set-alias-.md)の本文内の行の先頭のコマンドは、 [ **.foreach** ](-foreach.md)ループします。 行が始まるときに、**として**を使用して、エイリアスとトークンの行は展開されません。 セミコロンまたは前に空白を配置した場合、**として**コマンドを任意のエイリアスまたは値が既にトークンを展開します。 この例では、値が既にはないため myAlias は展開されません。 5 の値があるため、トークンが展開されます。 前にセミコロンを追加すると、同じ一連のコマンドを次に示します、**として**コマンド。

```dbgcmd
r $t0 = 5
ad myAlias
.foreach /pS 2 /ps 2 (Token {?@$t0}) {;as myAlias Token}
al
```

これで、想定される出力を取得します。

```dbgcmd
  Alias            Value  
 -------          ------- 
 myAlias          5 
```

### <a name="span-idrecursivealiasesspanspan-idrecursivealiasesspanrecursive-aliases"></a><span id="recursive_aliases"></span><span id="RECURSIVE_ALIASES"></span>再帰的なエイリアス

固定名のエイリアスは、任意のエイリアスの定義で使用できます。 固定名のエイリアスの定義でという名前のユーザーのエイリアスを使用することもできます。 ただし、前にセミコロンを追加する必要するという名前のユーザーのエイリアスを別のユーザーという名前のエイリアスの定義を使用する、**として**または**として**エイリアス置換するか、コマンド、その行では発生しません。

この型の再帰的な定義を使用している各エイリアスは、使用するとすぐに変換されます。 たとえば、次の例が表示されます**3**ではなく、 **7**します。

```dbgcmd
0:000> r $.u2=2 
0:000> r $.u1=1+$u2 
0:000> r $.u2=6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

同様に、次の例を表示します**3**ではなく、 **7**します。

```dbgcmd
0:000> as fred 2 
0:000> r $.u1= 1 + fred 
0:000> as fred 6 
0:000> ? $u1 
Evaluate expression: 3 = 00000003
```

次の例は許可されてもし表示**9**します。

```dbgcmd
0:000> r $.u0=2 
0:000> r $.u0=7+$u0 
0:000> ? $u0
Evaluate expression: 9 = 00000009
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

エイリアスを使用するには、次の例のように、長であるか、または複雑なシンボル名を入力する必要はありませんように。

```dbgcmd
0:000> as Short usersrv!NameTooLongToWantToType
0:000> dw Short +8
```

次の例は前の例に似ていますが、固定名のエイリアスを使用します。

```dbgcmd
0:000> r $.u0=usersrv!NameTooLongToWantToType
0:000> dw $u0+8
```

マクロとして頻繁に使用するコマンドのエイリアスを使用できます。 次の例のインクリメント、 **eax**と**ebx** 2 倍を登録します。

```dbgcmd
0:000> as GoUp r eax=eax+1; r ebx=ebx+1
0:000> GoUp
0:000> GoUp
```

次の例では、エイリアスを使用して、コマンドの入力を簡略化します。

```dbgcmd
0:000> as Cmd "dd esp 14; g"
0:000> bp MyApi Cmd 
```

次の例は前の例に似ていますが、固定名のエイリアスを使用します。

```dbgcmd
0:000> r $.u5="dd esp 14; g"
0:000> bp MyApi $u5 
```

前の例の両方は、次のコマンドに相当します。

```dbgcmd
0:000> bp MyApi "dd esp 14; g"
```

### <a name="span-idtoolsinifilespanspan-idtoolsinifilespan-toolsini-file"></a><span id="tools_ini_file"></span><span id="TOOLS_INI_FILE"></span> Tools.ini ファイル

CDB、NTSD) での固定名のエイリアスを事前に定義することができます、 [tools.ini](configuring-tools-ini.md)ファイル。 固定名のエイリアスを事前に定義するには追加、 **$u**フィールド、 \[NTSD\]エントリは、次の例のようにします。

```ini
[NTSD]
$u1:_ntdll!_RtlRaiseException
$u2:"dd esp 14;g"
$u9:$u1 + 42
```

Tools.ini でという名前のユーザーのエイリアスを設定することはできません。

### <a name="span-idfixednamealiasesvsusernamedaliasesspanspan-idfixednamealiasesvsusernamedaliasesspanfixed-name-aliases-vs-user-named-aliases"></a><span id="fixed_name_aliases_vs__user_named_aliases"></span><span id="FIXED_NAME_ALIASES_VS__USER_NAMED_ALIASES"></span>固定名のエイリアスとします。という名前のユーザーのエイリアス

ユーザー名のエイリアスは固定という名前のエイリアスをより簡単に使用されます。 その定義の構文が簡単ですとを使用してそれらを一覧表示できます、 [ **al (一覧のエイリアス)** ](al--list-aliases-.md)コマンド。

その他のテキストの横にある使用される場合、修正という名前のエイリアスは置き換えられます。 その他のテキストの横になるときに置き換えられるという名前のユーザーのエイリアスをするためでそれを囲む、 [ **$ {} (別名インタープリター)** ](-------alias-interpreter-.md)トークンです。

という名前のユーザーのエイリアスを交換する前に固定名のエイリアスの置換が行われます。

 

 





