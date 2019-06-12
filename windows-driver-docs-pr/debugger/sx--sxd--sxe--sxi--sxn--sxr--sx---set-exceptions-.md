---
title: sx、sxd、sxe、sxi、sxn、sxr、sx- (例外の設定)
description: Sx のコマンドは、デバッグ対象のアプリケーションで例外が発生した場合、または特定のイベントが発生したときに、デバッガーが実行されるアクションを制御します。
ms.assetid: fdb5059f-e7d9-4e14-aa3d-030e72c30732
keywords:
- sx, sxd、sxe、sxi、sxn、sxr、sx - (例外の設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sx, sxd, sxe, sxi, sxn, sxr, sx- (Set Exceptions)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db9b92435bd60bde07fff905bb7af15337799f5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383004"
---
# <a name="sx-sxd-sxe-sxi-sxn-sxr-sx--set-exceptions"></a>sx、sxd、sxe、sxi、sxn、sxr、sx- (例外の設定)


**Sx * * *\** コマンドは、アプリケーションをデバッグ中、または特定のイベントが発生したときに例外が発生したときに、デバッガーが実行されるアクションを制御します。

```dbgcmd
sx 

sx{e|d|i|n} [-c "Cmd1"] [-c2 "Cmd2"] [-h] {Exception|Event|*} 

sx- [-c "Cmd1"] [-c2 "Cmd2"] {Exception|Event|*} 

sxr
```

## <a name="span-idddkcmdsetexceptionsdbgspanspan-idddkcmdsetexceptionsdbgspanparameters"></a><span id="ddk_cmd_set_exceptions_dbg"></span><span id="DDK_CMD_SET_EXCEPTIONS_DBG"></span>パラメーター


<span id="-c__Cmd1_"></span><span id="-c__cmd1_"></span><span id="-C__CMD1_"></span> **-c"** <em>Cmd1</em> **"**  
イベント、例外が発生した場合に実行されるコマンドを指定します。 このコマンドは、この例外がデバッガーを中断するかどうかに関係なく、この例外を処理する最初の機会が発生したときに実行されます。 囲む必要があります、 *Cmd1*引用符で囲まれた文字列。 この文字列は、セミコロンで区切られた複数のコマンドを含めることができます。 -C と引用符で囲まれたコマンド文字列間のスペースは省略可能です。

<span id="-c2_Cmd2_"></span><span id="-c2_cmd2_"></span><span id="-C2_CMD2_"></span> **-c2"** <em>Cmd2</em> **"**  
イベント、例外が発生し、ファースト チャンスで処理されない場合に実行されるコマンドを指定します。 このコマンドは、この例外がデバッガーを中断するかどうかに関係なく、この例外を処理する 2 番目のチャンスが発生したときに実行されます。 囲む必要があります、 *Cmd2*引用符で囲まれた文字列。 この文字列は、セミコロンで区切られた複数のコマンドを含めることができます。 領域間は、c2、引用符で囲まれたコマンド文字列は省略可能です。

<span id="_______-h______"></span><span id="_______-H______"></span> **-h**   
その中断状態ではなく、指定したイベントの処理状態を変更します。 場合*イベント*は**cc**、 **hc**、 **bpec**、または**ssec**を使用する必要はありません、 **-h**オプション。

<span id="_______Exception______"></span><span id="_______exception______"></span><span id="_______EXCEPTION______"></span> *例外*   
現在の基数でのコマンドの処理、例外番号を指定します。

<span id="_______Event______"></span><span id="_______event______"></span><span id="_______EVENT______"></span> *イベント*   
コマンドが機能するイベントを指定します。 これらのイベントは、短い省略名によって識別されます。 イベントの一覧は、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

<span id="______________"></span> **\\** *   
それ以外の場合に明示的に名前のないのすべての例外の影響を与える**sx**します。 明示的に名前付きの例外の一覧は、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

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
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

中断状態と処理の状態、すべてのイベント コードの説明については、すべてのイベントの既定の状態の一覧と、この状態を制御するその他の方法の詳細については、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

<a name="remarks"></a>注釈
-------

**Sx**コマンドが nonexception のすべてのイベントの一覧と、現在のプロセスの例外の一覧を表示し、デバッガーの例外やイベントの既定の動作を表示します。

**Sxe**、 **sxd**、 **sxn**、および**sxi**コマンドは、各例外とイベントのデバッガーの設定を制御します。

**Sxr**コマンドがすべての例外とイベントのフィルター状態を既定の設定にリセットします。 コマンドがクリアされますが、中断/続行のオプションが既定の設定にリセットされます具合です。

**Sx-** コマンドでは、処理の状態や、指定した例外イベントの中断状態は変更されません。 このコマンドは、初回コマンドまたは特定のイベントに関連付けられている次の例外コマンドを変更する場合はその他の変更を希望しない場合に使用できます。

含める場合は、 **-h**オプション (または、 **cc**、 **hc**、 **bpec**、または**ssec**イベントを指定)、**sxe**、 **sxd**、 **sxn**、および**sxi**コマンド コントロール、[処理ステータス](https://msdn.microsoft.com/library/windows/hardware/ff541490#handling-status)のイベントまたは例外。 その他のすべてのケースではこれらのコマンドを制御、[状態](https://msdn.microsoft.com/library/windows/hardware/ff541490#break-status)例外、またはイベントの。

中断状態を設定するとき、これらのコマンドは、次の影響を与えます。

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
<td align="left"><p><strong>break</strong></p>
<p><strong>(有効)</strong></p></td>
<td align="left"><p>この例外が発生したときに、ターゲットすぐにデバッガーを中断前に、その他のエラー ハンドラーがアクティブ化されます。 この種の処理と呼びます<em>初回</em>を処理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd</strong></p></td>
<td align="left"><p><strong>2 番目のチャンスの中断</strong></p>
<p><strong>(無効)</strong></p></td>
<td align="left"><p>(ただし、メッセージが表示されます)、デバッガーはこの型の初回の例外は中断されません。 その他のエラー ハンドラーは、この例外を記載していません、実行が停止され、ターゲットがデバッガーを中断します。 この種の処理と呼びます<em>2 番目のチャンス</em>を処理します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sxn</strong></p></td>
<td align="left"><p><strong>出力</strong></p>
<p><strong>(通知)</strong></p></td>
<td align="left"><p>この例外が発生したときに、対象アプリケーションは中断されませんデバッガーにまったくです。 ただし、この例外のユーザーに通知するメッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxi</strong></p></td>
<td align="left"><p><strong>無視します。</strong></p></td>
<td align="left"><p>この例外が発生して、対象アプリケーションは、デバッガーに中断されませんメッセージは表示されません。</p></td>
</tr>
</tbody>
</table>

 

処理状態を設定するとき、これらのコマンドは、次の影響を与えます。

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
<td align="left"><p><strong>処理</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときの処理と見なされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>sxd,sxn,sxi</strong></p></td>
<td align="left"><p><strong>処理されていません。</strong></p></td>
<td align="left"><p>イベントは、実行が再開されるときに処理されないと見なされます。</p></td>
</tr>
</tbody>
</table>

 

使用することができます、 **-h**オプションを組み合わせて、例外、イベントではありません。 このオプションを使用して**ch**、 **bpe**、または**sse**の処理状態を設定**hc**、 **bpec**、または**ssec**、それぞれします。 その他のすべてのイベントは、-h オプションを使用する場合、影響を与えません。

使用して、 **-c**または **-c2**でオプションを**hc**、 **bpec**、または**ssec**指定されたコマンドに関連付けます**ch**、 **bpe**、または**sse**、それぞれします。

次の例では、 **sxe**違反イベントの最初のチャンスを中断して、設定をその時点で実行される初回コマンドへのアクセスの中断状態を設定するコマンドを使用**r eax**. 次に、 **sx -** 、初回のコマンドを変更するコマンドを使用**r ebx**、処理状態を変更することがなく。 部分では、最後に、 **sx**アクセス違反イベントの現在の設定を示す、出力が表示されます。

```dbgcmd
0:000> sxe -c "r eax" av 

0:000> sx- -c "r ebx" av 

0:000> sx 
 av - Access violation - break - not handled
       Command: "r ebx"
  . . .  
```

 

 





