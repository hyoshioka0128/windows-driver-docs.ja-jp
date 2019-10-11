---
title: sx、sxd、sxe、sxi、sxn、sxr、sx- (例外の設定)
description: Sx * コマンドは、デバッグ中のアプリケーションで例外が発生した場合、または特定のイベントが発生した場合に、デバッガーが実行するアクションを制御します。
ms.assetid: fdb5059f-e7d9-4e14-aa3d-030e72c30732
keywords:
- sx、sxd、sxd、sxd、sxn、sxr、sx-(例外の設定) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sx, sxd, sxe, sxi, sxn, sxr, sx- (Set Exceptions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 844e14723f50a08759297f62d40ab5d283458634
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038064"
---
# <a name="sx-sxd-sxe-sxi-sxn-sxr-sx--set-exceptions"></a>sx、sxd、sxe、sxi、sxn、sxr、sx- (例外の設定)

**Sx**コマンドは、デバッグ中のアプリケーションで例外が発生したとき、または特定のイベントが発生したときに、デバッガーが実行するアクションを制御します。

```dbgcmd
sx

sx{e|d|i|n} [-c "Cmd1"] [-c2 "Cmd2"] [-h] {Exception|Event|*}

sx- [-c "Cmd1"] [-c2 "Cmd2"] {Exception|Event|*}

sxr
```

## <a name="span-idddk_cmd_set_exceptions_dbgspanspan-idddk_cmd_set_exceptions_dbgspanparameters"></a><span id="ddk_cmd_set_exceptions_dbg"></span><span id="DDK_CMD_SET_EXCEPTIONS_DBG"></span>パラメータ

<span id="-c__Cmd1_"></span><span id="-c__cmd1_"></span><span id="-C__CMD1_"></span> **-c "** <em>Cmd1</em> **"**  
例外またはイベントが発生した場合に実行されるコマンドを指定します。 この例外が発生するのは、この例外がデバッガーに中断されたかどうかに関係なく、この例外を最初に処理する機会があるときです。 *Cmd1*文字列は引用符で囲む必要があります。 この文字列には、セミコロンで区切られた複数のコマンドを含めることができます。 -C と引用符で囲まれたコマンド文字列の間のスペースは省略可能です。

<span id="-c2_Cmd2_"></span><span id="-c2_cmd2_"></span><span id="-C2_CMD2_"></span> **-c2 "** <em>Cmd2</em> **"**  
例外またはイベントが発生し、初回では処理されない場合に実行されるコマンドを指定します。 この例外を処理する2番目の機会が発生したときに、この例外がデバッガーに中断したかどうかに関係なく、このコマンドが実行されます。 *Cmd2*文字列は引用符で囲む必要があります。 この文字列には、セミコロンで区切られた複数のコマンドを含めることができます。 -C2 と引用符で囲まれたコマンド文字列の間のスペースは省略可能です。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**ブレークステータスではなく、指定されたイベントの処理状態を変更します。 *イベント*が**cc**、 **hc**、 **bpec**、または**ssec**の場合は、 **-h**オプションを使用する必要はありません。

<span id="_______Exception______"></span><span id="_______exception______"></span><span id="_______EXCEPTION______"></span>*例外*現在の基数で、コマンドが処理する例外番号を指定します。

<span id="_______Event______"></span><span id="_______event______"></span><span id="_______EVENT______"></span>*イベント*コマンドが動作するイベントを指定します。 これらのイベントは、短い省略形によって識別されます。 イベントの一覧については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」を参照してください。

<span id="______________"></span> **\*** それ以外の場合、 **sx**に明示的に指定されていないすべての例外に影響します。 明示的に名前が付けられた例外の一覧については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」を参照してください。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブデバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断状態と処理状態、すべてのイベントコードの説明、すべてのイベントの既定の状態の一覧、およびこの状態を制御するその他の方法の詳細については、「[例外とイベントの制御](controlling-exceptions-and-events.md)」を参照してください。

<a name="remarks"></a>コメント
-------

**Sx**コマンドは、現在のプロセスの例外の一覧と、すべての例外以外のイベントの一覧を表示し、各例外とイベントに対するデバッガーの既定の動作を表示します。

**Sxe**、 **sxe**、 **sxn**、および**sxe**コマンドは、各例外とイベントのデバッガー設定を制御します。

**Sxr**コマンドは、すべての例外とイベントフィルターの状態を既定の設定にリセットします。 コマンドはクリアされ、break および continue オプションは既定の設定にリセットされます。

**Sx**コマンドは、指定された例外またはイベントの処理状態またはブレークステータスを変更しません。 このコマンドは、特定のイベントに関連付けられている初回のコマンドまたは2回目のコマンドを変更するが、他のイベントを変更したくない場合に使用できます。

**-H**オプションを含めた場合 (または**cc**、 **hc**、 **bpec**、または**ssec**イベントが指定されている場合)、 **ssec**、 **ssec**、 **sxn**、および**ssec**コマンドは例外の[処理状態](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#handling-status)を制御します。またはイベント。 それ以外の場合、これらのコマンドは例外またはイベントの[ブレーク状態](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx#break-status)を制御します。

中断状態を設定すると、これらのコマンドの効果は次のようになります。

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
<td align="left"><p><strong>sxe</strong></p></td>
<td align="left"><p><strong>改</strong></p>
<p><strong>Enabled</strong></p></td>
<td align="left"><p>この例外が発生すると、他のエラーハンドラーがアクティブ化される前に、ターゲットは直ちにデバッガーに中断します。 この種の処理は、<em>初回</em>処理と呼ばれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd</strong></p></td>
<td align="left"><p><strong>2回目の中断</strong></p>
<p><strong>無効に</strong></p></td>
<td align="left"><p>デバッガーは、この型の初回例外では中断しません (メッセージが表示されます)。 他のエラーハンドラーがこの例外に対処しない場合、実行が停止し、ターゲットがデバッガーに分割されます。 この種の処理は、 <em>2 回目</em>の処理と呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sxn</strong></p></td>
<td align="left"><p><strong>Output</strong></p>
<p><strong>報告</strong></p></td>
<td align="left"><p>この例外が発生した場合、ターゲットアプリケーションはデバッガーに中断されません。 ただし、この例外をユーザーに通知するメッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxi</strong></p></td>
<td align="left"><p><strong>かまい</strong></p></td>
<td align="left"><p>この例外が発生した場合、ターゲットアプリケーションはデバッガーを中断せず、メッセージも表示されません。</p></td>
</tr>
</tbody>
</table>

処理状態を設定すると、これらのコマンドには次のような影響があります。

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
<td align="left"><p><strong>sxe</strong></p></td>
<td align="left"><p><strong>対応</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときに処理されたと見なされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd、sxn、sxd</strong></p></td>
<td align="left"><p><strong>未処理</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときに処理されないと見なされます。</p></td>
</tr>
</tbody>
</table>

**-H**オプションは、イベントではなく例外と共に使用できます。 このオプションを**ch**、 **bpe**、または**sse**と共に使用すると、 **hc**、 **bpec**、または**ssec**の処理状態がそれぞれ設定されます。 他のイベントと共に-h オプションを使用しても、何の影響もありません。

**-C**または **-c2**オプションを**hc**、 **bpec**、または**ssec**と共に使用すると、指定したコマンドがそれぞれ**ch**、 **bpe**、または**sse**に関連付けられます。

次の例では、 **sxe**コマンドを使用して、最初の機会に中断するアクセス違反イベントのブレークステータスを設定し、その時点で実行されるファーストチャンスコマンドを**r eax**に設定します。 次に、 **sx**コマンドを使用して、ファーストチャンスのコマンドを**r ebx**に変更します。処理の状態は変更しません。 最後に、 **sx**出力の一部が表示されます。これは、アクセス違反イベントの現在の設定を示しています。

```dbgcmd
0:000> sxe -c "r eax" av

0:000> sx- -c "r ebx" av

0:000> sx
 av - Access violation - break - not handled
       Command: "r ebx"
  . . .  
```
