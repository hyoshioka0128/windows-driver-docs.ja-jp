---
title: list
description: リストの拡張機能、指定されたデバッガー コマンドを繰り返し実行、1 回リンク リスト内の各要素。
ms.assetid: 763742f3-1cb8-4263-861b-b9d01483245e
keywords:
- Windows デバッグ リスト
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cbd26bdccc2b040a85939746860817aeb175f461
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336198"
---
# <a name="list"></a>!list


**! 一覧**拡張機能、指定されたデバッガー コマンドを繰り返し実行、1 回、リンク リスト内の各要素。

```dbgcmd
!list -t [Module!]Type.Field -x "Commands" [-a "Arguments"] [Options] StartAddress 
!list " -t [Module!]Type.Field -x \"Commands\" [-a \"Arguments\"] [Options] StartAddress " 
!list -h 
```

## <a name="span-idddklistdbgspanspan-idddklistdbgspanparameters"></a><span id="ddk__list_dbg"></span><span id="DDK__LIST_DBG"></span>パラメーター


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
この構造体を定義するモジュールを指定する、省略可能なパラメーター。 可能性がある場合を*型*有効なシンボルが一致する別のモジュールに含める必要があります*モジュール*あいまいさを排除します。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
データ構造の名前を指定します。

<span id="_______Field______"></span><span id="_______field______"></span><span id="_______FIELD______"></span> *フィールド*   
一覧のリンクを含むフィールドを指定します。 ピリオドで区切られたフィールドのシーケンスを実際にはこのことができます (つまり、 **Type.Field.Subfield.Subsubfield**など)。

<span id="_______-x__Commands_"></span><span id="_______-x__commands_"></span><span id="_______-X__COMMANDS_"></span> **-x"**<em>コマンド</em>**"**  
実行するコマンドを指定します。 デバッガーのコマンドの任意の組み合わせを指定できます。 引用符で囲む必要があります。 場合は複数のコマンドを指定すると、独立したセミコロンを使用して囲みますのコレクション全体 **! 一覧**引用符とエスケープ文字を使用して引数 ( \\ ) 内でこれらの外部の各引用符の前に引用符がある場合。 場合*コマンド*は省略すると、既定値は[ **dp (表示メモリ)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)します。

<span id="_______-a__Arguments_"></span><span id="_______-a__arguments_"></span><span id="_______-A__ARGUMENTS_"></span> **-"**<em>引数</em>**"**  
渡す引数を指定します、*コマンド*パラメーター。 これは、引用符で囲む必要があります。 *引数*は、任意の有効な引数文字列に従うことを除いて、このコマンドが許可される通常*引数*引用符を含めることはできません。 場合、擬似レジスタ **$extret**に含まれている*コマンド*、 **-a"**<em>引数</em>**"** パラメーターを省略できます。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の数を指定できます。

<span id="-e"></span><span id="-E"></span>**-e**  
各要素に対して実行されているコマンドをエコーします。

<span id="-m_Max"></span><span id="-m_max"></span><span id="-M_MAX"></span>**-m** *Max*  
コマンドを実行する要素の最大数を指定します。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
最初のデータ構造体のアドレスを指定します。 これは、リンク フィールドのアドレスではなく、構造体の上部にあるアドレスです。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**! 一覧**拡張機能はリンク リストを移動し、各リスト要素に対して 1 回、指定したコマンドを発行します。

擬似レジスタ **$extret**リスト エントリのアドレスを各リスト要素の値に設定されます。 コマンド文字列は、各要素の*コマンド*を実行します。 このコマンド文字列は、この擬似レジスタを使用して参照できます、 **$extret**構文。 これは、コマンド文字列には表示されない場合がある場合は、実行する前にコマンド文字列の末尾に、リスト エントリのアドレスの値が追加されます。 コマンドでこの値を表示されますを指定する必要がある場合は、この擬似レジスタを明示的に指定する必要があります。

このコマンド シーケンスは、一覧が null ポインターで終了しますか、最初の要素に戻って、ループを終了までに実行されます。 一覧をループに戻って、後で要素をこのコマンドは停止されません。 使用して、いつでもでもこのコマンドを停止するただし、 [ **CTRL + C** ](ctrl-c--break-.md)で KD、CDB、または[デバッグ |中断](debug---break.md)または CTRL + BREAK WinDbg でします。

コマンドが実行されるたび、現在の構造体のアドレスとして使用される、*の既定の address*パラメーターを省略可能なアドレスが使用されているコマンドである場合。

ユーザー モードでこのコマンドを使用する方法の 2 つの例を次に示します。 カーネル モードの使用率も可能ですが、別の構文に注意してください。

単純な例としてには、型名を持つ、構造体を使用するいると仮定**MYTYPE**、内のリンクがその **.links します。Flink**と **.links します。点滅**フィールド。 0x6BC000 の構造で始まるリンク リストがあります。 次の拡張機能コマンド一覧を通過し、各要素に対して実行する[ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) L2 コマンド。 指定されているアドレスがないため、 **dd**コマンド、目的のアドレスとしてリストの先頭のアドレスになります。 これは、表示するには、各構造で最初の 2 つの Dword をによりします。

```dbgcmd
0:000> !list -t MYTYPE.links.Flink -x "dd" -a "L2" 0x6bc00 
```

複雑な例としてを使用する場合を考えてみましょう。 **$extret**します。 型の一覧を次に\_一覧\_位置にあるエントリ**RtlCriticalSectionList**します。 各要素に対して、最初の 4 つの DWORD を表示し、表示、 \_RTL\_重大\_セクション\_デバッグ構造体がより前のバージョンの 8 バイトのオフセットにある、 **Flink**一覧のエントリの要素。

```dbgcmd
0:000> !list "-t ntdll!_LIST_ENTRY.Flink -e -x \"dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8\" ntdll!RtlCriticalSectionList"
dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8
7c97c0c8  7c97c428 7c97c868 01010000 00000080
   +0x000 Type             : 1
   +0x002 CreatorBackTraceIndex : 0
   +0x004 CriticalSection  : (null)
   +0x008 ProcessLocksList : _LIST_ENTRY [ 0x7c97c428 - 0x7c97c868 ]
   +0x010 EntryCount       : 0x1010000
   +0x014 ContentionCount  : 0x80
   +0x018 Spare            : [2] 0x7c97c100

dd @$extret l4; dt ntdll!_RTL_CRITICAL_SECTION_DEBUG @$extret-0x8
7c97c428  7c97c448 7c97c0c8 00000000 00000000
   +0x000 Type             : 0
   +0x002 CreatorBackTraceIndex : 0
   +0x004 CriticalSection  : 0x7c97c0a0
   +0x008 ProcessLocksList : _LIST_ENTRY [ 0x7c97c448 - 0x7c97c0c8 ]
   +0x010 EntryCount       : 0
   +0x014 ContentionCount  : 0
   +0x018 Spare            : [2] 0
```

 

 





