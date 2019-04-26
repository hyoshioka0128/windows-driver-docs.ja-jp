---
title: .frame (ローカル コンテキストの設定)
description: .Frame コマンドでは、ローカル コンテキスト (スコープ) を使用して、ローカル変数の解釈を指定または、現在のローカル コンテキストが表示されます。
ms.assetid: eb843712-204f-4bbd-b711-a10756c9279a
keywords:
- ローカル コンテキスト (.frame) コマンドを設定します。
- メモリ、ローカル コンテキストの設定 (.frame) コマンド
- コンテキスト、ローカル コンテキストの設定 (.frame) コマンド
- .frame (ローカル コンテキストの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .frame (Set Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed2e2c3306edd234b46b96ba3f4ded323a545da7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336675"
---
# <a name="frame-set-local-context"></a>.frame (ローカル コンテキストの設定)


**.Frame**コマンドは、ローカル コンテキスト (スコープ) を使用して、ローカル変数の解釈を指定または現在のローカル コンテキストが表示されます。

```dbgcmd
.frame [/c] [/r] [FrameNumber] 
.frame [/c] [/r] = BasePtr [FrameIncrement] 
.frame [/c] [/r] = BasePtr StackPtr InstructionPtr 
```

## <a name="span-idddkmetasetlocalcontextdbgspanspan-idddkmetasetlocalcontextdbgspanparameters"></a><span id="ddk_meta_set_local_context_dbg"></span><span id="DDK_META_SET_LOCAL_CONTEXT_DBG"></span>パラメーター


<span id="________c______"></span><span id="________C______"></span> **/c**   
現在のローカル上書きコンテキストとして指定したフレームを設定します。 このアクションでは、呼び出し履歴の関数の不揮発性レジスタにアクセスするユーザー。

<span id="________r______"></span><span id="________R______"></span> **/r**   
レジスタ、および指定したローカル コンテキストの詳細については、その他の情報が表示されます。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span> *FrameNumber*   
フレームをローカル コンテキストの数を指定します。 このパラメーターが 0 の場合、コマンドには、現在のフレームを指定します。 このパラメーターを省略した場合、このコマンドは、現在のローカル コンテキストを表示します。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span> *BasePtr*   
コマンド名の後に等号 (=) を追加する場合、フレームを決定に使用されるスタック トレースの基本ポインターを指定します (**.frame**)。 X86 ベースのプロセッサでは、後にもう 1 つの引数を追加する*BasePtr* (として解釈される*FrameIncrement*) または後に複数の引数を 2 つ*BasePtr* (として解釈*InstructionPtr*と*StackPtr*)。

<span id="_______FrameIncrement______"></span><span id="_______frameincrement______"></span><span id="_______FRAMEINCREMENT______"></span> *FrameIncrement*   
(x86 プロセッサのみ)

過去の基本ポインターのフレームの追加の数量を指定します。 たとえば、次の基本ポインター 0x0012FF00 フレーム 3、コマンドのアドレスは、 **.frame 12ff00**と等価 **.frame 3**、および **.frame 12ff00 2** と等価 **.frame 5**します。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span> *StackPtr*   
(x86 プロセッサのみ)フレームを決定するために使用するスタック トレースのスタック ポインターを指定します。 省略した場合*StackPtr*と*InstructionPtr*、デバッガーはスタック ポインターを使用する、 **esp**レジスタを指定と命令ポインターを**eip**レジスタを指定します。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span> *InstructionPtr*   
(x86 プロセッサのみ)フレームを決定するために使用するスタック トレースの命令ポインターを指定します。 省略した場合*StackPtr*と*InstructionPtr*、デバッガーはスタック ポインターを使用する、 **esp**レジスタを指定と命令ポインターを**eip**レジスタを指定します。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ローカル コンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 ローカル変数とその他のメモリに関連するコマンドを表示する方法の詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>注釈
-------

アプリケーションが実行されているときに、ローカル変数の意味で定義されている関数にのみこのような変数のスコープを拡張するため、プログラム カウンターの場所に依存します。 使用しない場合、 **.frame**コマンド、デバッガーは、現在の関数 (スタック上の現在のフレーム) のスコープとして、[ローカル コンテキスト](changing-contexts.md#local-context)します。

ローカル コンテキストを変更するには、使用、 **.frame**コマンドを使用するフレームの数を指定します。

*フレーム番号*はスタック トレース内でスタック フレームの位置です。 このスタック トレースを表示することができます、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドまたは[コール スタック ウィンドウ](calls-window.md)します。 最初の行 (現在のフレーム) は、フレーム番号 0 です。 それ以降の行は、フレーム番号 1、2、3 を表し、具合です。

使用する場合、 **n**パラメーター、 [ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド、 **k**コマンドと共に、スタック トレース フレーム番号を表示します。 これらのフレーム番号は常に 16 進数形式で表示されます。 一方で、 **.frame** 0 x などのプレフィックスでは、この設定を上書きしない限り、コマンドが既定の基数での引数を解釈します。 既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

新しいローカル変数の情報を表示するための別のスタック フレームには、ローカル コンテキストを設定できます。 ただし、使用できる実際の変数は、実行されているコードに依存します。

ローカル コンテキストは、任意のアプリケーションの実行が発生した場合、プログラム カウンターのスコープにリセットされます。 ローカル コンテキストは、レジスタのコンテキストが変更された場合、最上位のスタック フレームにリセットされます。

 

 





