---
title: z (While の実行)
description: Z コマンドは、指定された条件が true の場合のコマンドを実行します。
ms.assetid: 075dc012-68c2-4172-9d37-57bc8358297c
keywords:
- z (実行中に) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- z (Execute While)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24447078209a4c97c2d359c9ccf1b3c9c1974d93
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381893"
---
# <a name="z-execute-while"></a>z (While の実行)


**Z**が特定の条件が true の場合、コマンドがコマンドを実行します。

ユーザー モード

```dbgcmd
Command ; z( Expression ) 
```

カーネル モード

```dbgcmd
Command ; [Processor] z( Expression )
```

## <a name="span-idddkcmdexecutewhiledbgspanspan-idddkcmdexecutewhiledbgspanparameters"></a><span id="ddk_cmd_execute_while_dbg"></span><span id="DDK_CMD_EXECUTE_WHILE_DBG"></span>パラメーター


<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
実行するコマンドを指定します。 中に、*式*条件の評価が 0 以外の値。 このコマンドは常に少なくとも 1 回に実行します。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
テストに適用されるプロセッサを指定します。 構文の詳細については、次を参照してください。[マルチプロセッサ構文](multiprocessor-syntax.md)します。 プロセッサは、カーネル モードでのみ指定できます。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
テストする条件を指定します。 この条件は、0 以外の値に評価された場合、*コマンド*コマンドをもう一度実行し、*式*をもう一度テストします。 構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

多くのデバッガー コマンドでは、関連のないコマンドを分離する、セミコロンを使用します。 ただしでは、 **z**からのコマンド、"z"をセミコロンで区切って、*コマンド*パラメーター。

*コマンド*コマンドは常に少なくとも 1 回実行し、*式*をテストします。 条件が 0 以外の値の場合は、コマンドをもう一度実行、し*式*をもう一度テストします。 (この動作は C 言語のような**do -** ループでない単純な**中に**ループします)。

"Z"繰り返し long としてとしての左側に"z"の左側にいくつかセミコロンがある場合は、すべてのコマンド、*式*条件が true です。 このようなコマンドでは、ターミナルのセミコロンを許可する任意のデバッガー コマンドを指定できます。

もう 1 つのセミコロンと後にその他のコマンドを追加する場合、 **z**コマンド、ループが完了したら、次のコマンドは実行されます。 通常しないでが生成されるため不要な出力永遠にその他のいくつかの操作により、条件が false になる場合を除き、"z"で始まる行。 入れ子にすることに注意してください**z**コマンド。

長期間継続するループを中断するには使用[ **CTRL + C** ](ctrl-c--break-.md) CDB、KD、または使用[デバッグ |中断](debug---break.md)または CTRL + BREAK WinDbg でします。

次のコード例は、0、不必要に複雑な方法を示しています、 **eax**を登録します。

```dbgcmd
0:000> reax = eax - 1 ; z(eax)
```

次の例のインクリメント、 **eax**と**ebx** 8 では、少なくとも 1 つはまで増加し、登録、 **ecx**を 2 回登録します。

```dbgcmd
0:000> reax=eax+1; rebx=ebx+1; z((eax<8)|(ebx<8)); recx=ecx+1
```

次の例は、C++ 式の構文を使用し、擬似レジスタを使用して **$t0**ループ変数として。

```dbgcmd
0:000> .expr /s c++
Current expression evaluator: C++ - C++ source expressions

0:000> db pindexcreate[@$t0].szKey; r$t0=@t0+1; z( @$t0 < cIndexCreate )
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**j (If-else を実行する場合)**](j--execute-if---else-.md)

 

 






