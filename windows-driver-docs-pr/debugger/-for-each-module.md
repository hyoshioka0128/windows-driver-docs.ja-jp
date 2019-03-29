---
title: for_each_module
description: For_each_module 拡張機能は、読み込まれたモジュールごとに 1 回デバッガー コマンドを実行します。
ms.assetid: 607947d8-be06-4012-8901-13bf27e382b1
keywords:
- Windows デバッグ for_each_module
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_module
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4455402ce1b2b061449c54cad58983e89077f7b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572674"
---
# <a name="foreachmodule"></a>! の\_各\_モジュール


**! の\_各\_モジュール**拡張機能は読み込まれたモジュールごとに 1 回のデバッガー コマンドを実行します。

```dbgcmd
!for_each_module ["CommandString"]
!for_each_module -?
```

## <a name="span-idddkforeachmoduledbgspanspan-idddkforeachmoduledbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>パラメーター


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
デバッガーのモジュールの一覧で、モジュールごとに 1 回を実行するデバッガー コマンドを指定します。 場合*クラスヒント*複数のコマンドが含まれていますをセミコロンで区切るしで囲む必要があります*クラスヒント*引用符で囲んで指定します。 各コマンドの中で複数のコマンドを含める場合*クラスヒント*引用符を含めることはできません。

次のエイリアスを使用する*クラスヒント*またはいずれかでスクリプトをコマンドでは、*クラスヒント*を実行します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Alias</th>
<th align="left">データ型</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@# FileVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>モジュールのファイル バージョン。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# ProductVersion</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>モジュールの製品のバージョン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModuleIndex</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>モジュールの数。 モジュールは、ゼロから始まり、連続して列挙されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#ModuleName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>モジュール名。 この名前は、通常、ファイル名拡張子を除いたファイル名です。 場合によっては、モジュール名はファイル名から大幅に異なります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@# ImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ファイル名拡張子を含む、実行可能ファイルの名前。 通常、完全なパスが含まれるカーネル モードではなくユーザー モードにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#LoadedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Microsoft CodeView シンボルが存在しない限り、このエイリアスは、イメージの名前と同じになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#MappedImageName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>このエイリアスは、ほとんどの状況で<strong>NULL</strong>します。 マップする場合、デバッガーは、イメージ ファイル (たとえば、ミニダンプ デバッグの実行) 中、このエイリアスは、マップされたイメージの名前です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#SymbolFileName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パスとシンボル ファイルの名前。 このエイリアスをすべてのシンボルが読み込まれていない場合、実行可能ファイルの名前が代わりにです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModuleNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>モジュール名の文字列と 1 つの文字列の長さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# ImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>イメージ名の文字列と 1 つの文字列の長さ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#LoadedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>読み込まれたイメージ名の文字列と 1 つの文字列の長さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#MappedImageNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>マップされたイメージ名の文字列と 1 つの文字列の長さ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#SymbolFileNameSize</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>シンボル ファイル名の文字列と 1 つの文字列の長さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# Base</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>イメージの開始アドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@# Size</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>イメージには、バイトのサイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# End</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>イメージの最後のアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@# TimeDateStamp</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>イメージの日付と時刻のタイムスタンプ。 判読可能な日付にこの日付と時刻のスタンプを展開する場合は、使用、 <strong><a href="-formats--show-number-formats-.md" data-raw-source="[.formats (Show Number Formats)](-formats--show-number-formats-.md)">(番号の形式の表示) .formats</a></strong>コマンド。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>@# Checksum</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>モジュールのチェックサム。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# Flags</p></td>
<td align="left"><p>ULONG</p></td>
<td align="left"><p>モジュールのフラグ。 DEBUG_MODULE_ の一覧については<em>Xxx</em>値、Dbgeng.h を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#SymbolType</p></td>
<td align="left"><p>USHORT</p></td>
<td align="left"><p>記号の型。 DEBUG_SYMTYPE_ の一覧については<em>Xxx</em>値、Dbgeng.h を参照してください。</p></td>
</tr>
</tbody>
</table>

 

これらのエイリアスはすべて前に置き換える*クラスヒント*モジュールごとに、およびその他の解析が発生する前に実行されます。 これらのエイリアスは、大文字小文字を区別します。 エイリアスがかっこで囲まれている場合でも、その後、エイリアスの前にスペースとスペースを追加する必要があります。 C++ 式の構文を使用する場合は、としてこれらの別名を参照しなければなりません。 @ (@\#*エイリアス*)。

呼び出しの有効期間中にのみ、これらのエイリアスは使用可能な **! の\_各\_モジュール**します。 擬似レジスタ、固定名のエイリアスまたはという名前のユーザーのエイリアスでそれらを混同ください。

<span id="_______-_______"></span> -?   
この拡張機能のいくつかのヘルプ テキストが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

定義および文字の文字列 ($ {} のトークンの使用を含む) を入力するためのショートカットとしてエイリアスを使用する方法の詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

<a name="remarks"></a>コメント
-------

任意の引数を指定しない場合、 **! の\_各\_モジュール**拡張機能が読み込まれたモジュールに関する一般的な情報が表示されます。 この情報は、次のコマンドが表示される情報に似ています。

```dbgcmd
!for_each_module .echo @#ModuleIndex : @#Base @#End @#ModuleName @#ImageName  @#LoadedImageName
```

読み込まれ、モジュールをアンロードについての詳細については、使用、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)コマンド。

拡張機能が呼び出され、デバッガーする前に各モジュール(使用可能な各エイリアスの値を含む)に関する詳細情報が表示されます、デバッガーが読み込まれ、アンロードされたモジュールの合計数を表示のデバッガーの詳細な出力を有効にした場合*クラスヒント*モジュールに対して実行されます。

次の例を使用する方法を示して、 **! の\_各\_モジュール**拡張機能。 次のコマンドは、グローバル デバッグ フラグを表示します。

```dbgcmd
!for_each_module x ${@#ModuleName}!*Debug*Flag*
!for_each_module x ${@#ModuleName}!g*Debug*
```

次のコマンドを使用して、すべての読み込まれたモジュールのバイナリが破損していないを確認します。、 [ **! chkimg** ](-chkimg.md)拡張機能。

```dbgcmd
!for_each_module !chkimg @#ModuleName
```

次のコマンドは、すべての読み込まれたイメージのパターン"MZ"を検索します。

```dbgcmd
!for_each_module s-a @#Base @#End "MZ"
```

次の例は、@ の使用を示します\#FileVersion および @\#ProductVersion の各モジュールの名前。

```dbgcmd
0:000> !for_each_module .echo @#ModuleName fver = @#FileVersion pver = @#ProductVersion 
USER32 fver = 6.0.6000.16438 (vista_gdr.070214-1610) pver = 6.0.6000.16438
kernel32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
ntdll fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
notepad fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
WINSPOOL fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
COMCTL32 fver = 6.10 (vista_rtm.061101-2205) pver = 6.0.6000.16386
SHLWAPI fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
msvcrt fver = 7.0.6000.16386 (vista_rtm.061101-2205) pver = 7.0.6000.16386
GDI32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
RPCRT4 fver = 6.0.6000.16525 (vista_gdr.070716-1600) pver = 6.0.6000.16525
SHELL32 fver = 6.0.6000.16513 (vista_gdr.070626-1505) pver = 6.0.6000.16513
ole32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
ADVAPI32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
COMDLG32 fver = 6.0.6000.16386 (vista_rtm.061101-2205) pver = 6.0.6000.16386
```

 

 





