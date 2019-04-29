---
title: lm (読み込まれたモジュールの一覧表示)
description: Lm コマンドは、指定された読み込み済みモジュールを表示します。 出力には、状態と、モジュールのパスが含まれています。
ms.assetid: ee2283bd-4d3f-4e30-8b32-e286a415bb3a
keywords:
- lm (読み込まれたモジュールを一覧表示) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lm (List Loaded Modules)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 803d08868069781f43eec4c951818d80fafaec2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383392"
---
# <a name="lm-list-loaded-modules"></a>lm (読み込まれたモジュールの一覧表示)


**Lm**コマンドは、指定された読み込み済みモジュールを表示します。 出力には、状態と、モジュールのパスが含まれています。

```dbgcmd
lm Options [a Address] [m Pattern | M Pattern]
```

## <a name="span-idddkcmdlistloadedmodulesdbgspanspan-idddkcmdlistloadedmodulesdbgspanparameters"></a><span id="ddk_cmd_list_loaded_modules_dbg"></span><span id="DDK_CMD_LIST_LOADED_MODULES_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせには:

<span id="D"></span><span id="d"></span>D  
出力を使用して表示[デバッガー Markup Language](debugger-markup-language-commands.md)します。

<span id="o"></span><span id="O"></span>O  
読み込まれたモジュールのみを表示します。

<span id="l"></span><span id="L"></span>L  
シンボル情報が読み込まれたモジュールのみを表示します。

<span id="v"></span><span id="V"></span>v  
詳細情報の表示をによりします。 シンボルのファイル名、イメージ ファイル名、チェックサム情報、バージョン情報、日付スタンプ、タイムスタンプ、およびモジュールが管理されているかどうかに関する情報が含まれるコード (CLR)。 関連するヘッダーが見つからないかアウト ページングされた場合、この情報は表示されません。

<span id="u"></span><span id="U"></span>u  
(カーネル モードのみ)ユーザー モードのシンボル情報のみが表示されます。

<span id="k"></span><span id="K"></span>k  
(カーネル モードのみ)カーネル モードのシンボル情報のみが表示されます。

<span id="e"></span><span id="E"></span>e  
シンボルの問題があるモジュールのみを表示します。 これらのシンボルは、モジュールがないシンボルがシンボルの状態は、C、T、モジュール\#M、またはエクスポートします。 これらの表記の詳細については、次を参照してください。[シンボルの状態の省略形](symbol-status-abbreviations.md)します。

<span id="c"></span><span id="C"></span>c  
チェックサム データを表示します。

<span id="1m"></span><span id="1M"></span>1 m  
何がモジュールの名前を除く含まれるように、出力が減少します。 このオプションを使用している場合に便利ですが、 [ **.foreach** ](-foreach.md)コマンドの出力を別のコマンドにパイプするためのトークンの入力します。

<span id="sm"></span><span id="SM"></span>sm  
開始アドレスでは、モジュール名の代わりに、表示を並べ替えます。

さらに、次のオプションのいずれかのみを含めることができます。 これらのオプションのいずれかを指定しない場合、表示には、シンボルのファイル名が含まれます。

<span id="i"></span><span id="I"></span>i  
イメージ ファイル名が表示されます。

<span id="f"></span><span id="F"></span>f  
完全なイメージのパスが表示されます。 (このパスは、初期読み込みの通知に表示されるパスを常に一致を発行した場合を除き、 [ **.reload-s** ](-reload--reload-module-.md)コマンド)。F を使用すると、シンボルの種類の情報は表示されません。

<span id="n"></span><span id="N"></span>n  
イメージの名前が表示されます。 N を使用すると、シンボルの種類の情報は表示されません。

<span id="p"></span><span id="P"></span>P  
マップされたイメージの名前が表示されます。 P を使用すると、シンボルの種類の情報は表示されません。

<span id="t"></span><span id="T"></span>t  
ファイルのタイムスタンプが表示されます。 T を使用すると、シンボルの種類の情報は表示されません。

<span id="_______a_______Address______"></span><span id="_______a_______address______"></span><span id="_______A_______ADDRESS______"></span> *アドレス*   
このモジュールでは、格納されているアドレスを指定します。 このアドレスを格納しているモジュールのみが表示されます。 アドレスに式が含まれている場合は、かっこで囲む必要があります。

<span id="_______m_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> m*パターン*   
モジュール名に一致する必要があるパターンを指定します。 パターンは、さまざまなワイルドカード文字と指定子を含めることができます。 この情報の詳細、構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

**注**  ほとんどの場合、モジュール名はファイル名拡張子を除いたファイル名。 たとえば、Flpydisk.sys ドライバーに関する情報を表示する場合は、lm mflpydisk コマンド、lm mflpydisk.sys いないを使用します。 場合によっては、モジュール名はファイル名から大幅に異なります。

 

<span id="_______M_______Pattern______"></span><span id="_______m_______pattern______"></span><span id="_______M_______PATTERN______"></span> m*パターン*   
イメージのパスに一致する必要があるパターンを指定します。 パターンは、さまざまなワイルドカード文字と指定子を含めることができます。 この情報の詳細、構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Lm**コマンドは、すべてのモジュールと各モジュールのシンボルの状態を示します。

Microsoft Windows Server 2003 と以降のバージョンの Windows は、ユーザー モード プロセス用にアンロードされたモジュールの一覧を保持します。 ユーザー モード プロセスまたはダンプのファイルをデバッグするとき、 **lm**コマンドでは、これらのモジュールをアンロードも示しています。

このコマンドには、いくつかの列またはフィールドは、それぞれに別のタイトルが表示されます。 これらのタイトルの一部で、特定の意味があります。

-   *モジュール名*は通常のファイル名拡張子を除いたファイル名。 場合によっては、モジュール名はファイル名から大幅に異なります。

-   記号の型、モジュール名の直後にします。 この列はラベルが表示されません。 詳細については、さまざまな状態の値は、次を参照してください。[シンボルの状態の省略形](symbol-status-abbreviations.md)します。 シンボルを読み込んだ場合、シンボル ファイル名はこの列に従います。

-   モジュールの最初のアドレスは、スタートとして表示されます。 モジュールの最後は、終了と表示した後の最初のアドレス。 たとえば、開始が"faab4000"で末尾が"faab8000"の場合、モジュール拡張 0xFAAB4000 から 0xFAAB7FFF、包括的にします。

-   **lmv**のみ。イメージ パス 列では、ファイル名拡張子を含む、実行可能ファイルの名前を表示します。 通常、完全なパスが含まれるカーネル モードではなくユーザー モードにします。

-   **lmv**のみ。読み込まれたシンボル イメージ ファイルの値では、Microsoft CodeView シンボルが存在しない限り、イメージ名の場合と同じです。

-   **lmv**のみ。マップされたメモリのイメージ ファイルの値は通常使用されません。 マップする場合、デバッガーは、イメージ ファイル (たとえば、ミニダンプ デバッグの実行) 中、この値は、マップされたイメージの名前にします。

次のコード例は、 **lm**コマンドを Windows Server 2003 の対象コンピューターにします。 この例には、s、m が含まれます。\*オプションは、"s"で始まるのみモジュールが表示されるようにします。

```dbgcmd
kd> lm m s*
start    end        module name
f9f73000 f9f7fd80   sysaudio     (deferred)                 
fa04b000 fa09b400   srv          (deferred)                 
faab7000 faac8500   sr           (deferred)                 
facac000 facbae00   serial       (deferred)                 
fb008000 fb00ba80   serenum      e:\mysymbols\SereEnum.pdb\.......
fb24f000 fb250000   swenum       (deferred)                 

Unloaded modules:
f9f53000 f9f61000   swmidi.sys
fb0ae000 fb0b0000   splitter.sys
fb040000 fb043000   Sfloppy.SYS
```

<a name="examples"></a>例
--------

次の 2 つの例、 **lm**コマンド、オプションを 1 回し、1 回、sm オプションを使用します。 2 つの例の並べ替え順序を比較します。

例 1:

```dbgcmd
0:000> lm
start    end        module name
01000000 0100d000   stst       (deferred)
77c10000 77c68000   msvcrt     (deferred)
77dd0000 77e6b000   ADVAPI32   (deferred)
77e70000 77f01000   RPCRT4     (deferred)
7c800000 7c8f4000   kernel32   (deferred)
7c900000 7c9b0000   ntdll      (private pdb symbols) c:\db20sym\ntdll.pdb
```

例 2:

```dbgcmd
0:000> lmsm
start    end        module name
77dd0000 77e6b000   ADVAPI32   (deferred)
7c800000 7c8f4000   kernel32   (deferred)
77c10000 77c68000   msvcrt     (deferred)
7c900000 7c9b0000   ntdll      (private pdb symbols)  c:\db20sym\ntdll.pdb
77e70000 77f01000   RPCRT4     (deferred)
01000000 0100d000   stst       (deferred)
```

 

 





