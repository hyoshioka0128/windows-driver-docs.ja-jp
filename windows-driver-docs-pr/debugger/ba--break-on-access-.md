---
title: ba (アクセスの切断)
description: Ba コマンドでは、(多くの場合と呼ばれる、あまり正確には、データ ブレークポイント) プロセッサ ブレークポイントを設定します。 指定されたメモリにアクセスする場合は、このブレークポイントがトリガーされます。
ms.assetid: 0d39d883-363e-421b-a1b8-08bf2d216724
keywords:
- ba (アクセスの切断) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ba (Break on Access)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b47a8b7ca128f12293ad5a63c2d46e8ffb567d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556495"
---
# <a name="ba-break-on-access"></a>ba (アクセスの切断)


**Ba**コマンド プロセッサ ブレークポイントを設定 (多くの場合、呼び出されると、小さい正確を*データ ブレークポイント*)。 指定されたメモリにアクセスする場合は、このブレークポイントがトリガーされます。

ユーザー モード

```dbgcmd
[~Thread] ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

カーネル モード

```dbgcmd
ba[ID] Access Size [Options] [Address [Passes]] ["CommandString"]
```

## <a name="span-idddkcmdbreakonaccessdbgspanspan-idddkcmdbreakonaccessdbgspanparameters"></a><span id="ddk_cmd_break_on_access_dbg"></span><span id="DDK_CMD_BREAK_ON_ACCESS_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
ブレークポイントが適用されるスレッドを指定します。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
ブレークポイントを識別する任意の数を指定します。 指定しない場合*ID*、最初のブレークポイントの使用可能な番号が使用されます。 間にスペースを追加することはできません**ba**と ID 番号。 各プロセッサは、ブレークポイントのプロセッサの数に制限のみをサポートしていますの値に制限はありません、 *ID*数。 囲んだ場合*ID*角かっこで囲んで (\[\])、 *ID*任意の式を含めることができます。 構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="_______Access______"></span><span id="_______access______"></span><span id="_______ACCESS______"></span> *アクセス*   
ブレークポイントを満たすアクセスの種類を指定します。 このパラメーターは、次の値のいずれかを指定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>e</strong> (実行)</p></td>
<td align="left"><p>CPU が指定したアドレスから命令を取得するときにデバッガーを中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> (読み取り/書き込み)</p></td>
<td align="left"><p>CPU の読み取りまたは書き込み、指定したアドレスと、デバッガーを中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>w</strong> (書き込み)</p></td>
<td align="left"><p>指定したアドレスで、CPU を書き込むときにデバッガーを中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></strong> (i/o)</p></td>
<td align="left"><p>(カーネル モードのみ、x86 ベース システムのみ)I/O ポートの指定したときにデバッガーを中断<em>アドレス</em>にアクセスします。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *サイズ*   
(バイト単位) を監視するためのアクセスの場所のサイズを指定します。 X86 ベースのプロセッサでは、このパラメーターは 1、2、または 4 を指定できます。 ただし場合、*アクセス*equals **e**、*サイズ*1 である必要があります。

X64 ベースのプロセッサでは、このパラメーターは 1、2、4、または 8 を指定できます。 ただし場合、*アクセス*equals **e**、*サイズ*1 である必要があります。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
ブレークポイントのオプションを指定します。 とおりを除く任意の数の次のオプションを使用できます。

<span id="_1"></span>**/1**  
「ワンショット」のブレークポイントを作成します。 このブレークポイントがトリガーされた後、ブレークポイントはブレークポイントの一覧から完全に削除します。

<span id="_p_EProcess"></span><span id="_p_eprocess"></span><span id="_P_EPROCESS"></span>**/p** *」プロセス*  
(カーネル モードのみ)このブレークポイントに関連付けられているプロセスを指定します。 *」プロセス*」プロセスの構造、PID ではないの実際のアドレスにする必要があります。 このプロセスのコンテキストで検出された場合にのみ、ブレークポイントがトリガーされます。

<span id="_t_EThread"></span><span id="_t_ethread"></span><span id="_T_ETHREAD"></span>**/t** *EThread*  
(カーネル モードのみ)このブレークポイントに関連付けられているスレッドを指定します。 *EThread* ETHREAD 構造体、スレッド ID ではないの実際のアドレスにする必要があります これがこのスレッドのコンテキストで発生した場合にのみ、ブレークポイントがトリガーされます。 使用する場合 **/p** *」プロセス*と **/t** *EThread* 、任意の順序で入力することができます。

<span id="_c_MaxCallStackDepth"></span><span id="_c_maxcallstackdepth"></span><span id="_C_MAXCALLSTACKDEPTH"></span>**/c** *MaxCallStackDepth*  
ブレークポイントを呼び出しスタックの深さが場合にのみアクティブにするより小さい*MaxCallStackDepth*します。 と共にこのオプションを組み合わせることはできません **/C**します。

<span id="_C_MinCallStackDepth"></span><span id="_c_mincallstackdepth"></span><span id="_C_MINCALLSTACKDEPTH"></span>**/C** *MinCallStackDepth*  
呼び出しスタックの深さがより大きい場合にのみアクティブにするブレークポイントを発生*MinCallStackDepth*します。 と共にこのオプションを組み合わせることはできません **/c**します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
有効なアドレスを指定します。 アプリケーションでは、このアドレスにアクセスする、デバッガーは実行を停止し、すべてのレジスタとフラグの現在の値が表示されます。 このアドレスは、オフセットとを適切にアライメントされた一致である必要があります、*サイズ*パラメーター。 (たとえば、*サイズ*は 4、*アドレス*4 の倍数である必要があります)。省略した場合*アドレス*、現在の命令ポインターを使用します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Passes______"></span><span id="_______passes______"></span><span id="_______PASSES______"></span> *パス*   
ブレークポイントがアクティブになるまでによって渡される回数を指定します。 この数は 16 ビット値を指定できます。 プログラム カウンターは、互換性に影響はなくこのポイントを通過回数の合計この数値の値より小さくします。 そのため、この番号を省略すると、1 と等しく設定と同じです。 この数が時刻のみをカウントにも注意してくださいをアプリケーション*実行*このポイント以降。 ステップ実行または時点からこのトレースはカウントされません。 フル カウントに達すると、クリアし、ブレークポイントをリセットすることによってのみ、この番号をリセットできます。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
ブレークポイントがあるたびに実行するコマンドの一覧に発生した指定した回数を指定します。 発行した後、ブレークポイントにヒットする場合にのみ、これらのコマンドが実行される、 [ **g (移動)** ](g--go-.md)後の代わりにコマンドを[ **t (トレース)** ](t--trace-.md)または[ **p (ステップ)** ](p--step-.md)コマンド。 デバッガーでのコマンド*クラスヒント*パラメーターを含めることができます。

このコマンド文字列を引用符で囲む必要があり、セミコロンで複数のコマンドを分離する必要があります。 標準 C 制御文字を使用することができます (など **\\n**と **\\"**)。 引用符を 2 番目のレベルに格納されているセミコロン (**\\"**) 文字列を引用符で囲まれた、埋め込みの一部として解釈されます。

このパラメーターは省略可能です。

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

プロセッサのブレークポイントの詳細については、次を参照してください。[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)します。 詳細とブレークポイント、他のコマンドのブレークポイントとブレークポイント、およびカーネル デバッガーからのユーザー領域でブレークポイントを設定する方法に関する情報を制御する方法を使用する例については、次を参照してください[を使用してブレークポイント](using-breakpoints.md). 条件付きブレークポイントの詳細については、次を参照してください。 [、条件付きブレークポイント](setting-a-conditional-breakpoint.md)します。

<a name="remarks"></a>注釈
-------

デバッガーを使用して、 *ID*内のブレークポイントを後で参照する数[ **bc (ブレークポイント クリア)**](bc--breakpoint-clear-.md)、 [ **(ブレークポイントを無効にする)bd**](bd--breakpoint-disable-.md)、および[ **(ブレークポイントを有効にする) をある**](be--breakpoint-enable-.md)コマンド。

使用して、 [ **bl (ブレークポイントの一覧)** ](bl--breakpoint-list-.md)既存のすべてのブレークポイント、ID 番号、およびそれらの状態を一覧表示するコマンド。

使用して、 [ **.bpcmds (ブレークポイント コマンドが表示)** ](-bpcmds--display-breakpoint-commands-.md)既存のすべてのブレークポイント、ID 番号、およびその作成に使用されたコマンドを一覧表示するコマンド。

各プロセッサのブレークポイントでは、関連付けられているサイズがあります。 たとえば、 **w** (書き込み) はサイズが 4 バイトのアドレス 0x70001008 でプロセッサのブレークポイントを設定できます。 これは、モニターは 0x7000100B、包括的に 0x70001008 からアドレスのブロックは、します。 メモリのブロックが書き込まれる、ブレークポイントがトリガーされます。

プロセッサがメモリ領域での操作を実行する可能性を*と重複*とではない、指定した領域に同じです。 この例では、1 回の書き込み 0x70001000 に 0x7000100F 範囲を含む操作または 0x70001009、位置にあるバイトだけを含む書き込み操作は、重複する操作になります。 このような状況ではプロセッサに依存するには、ブレークポイントがトリガーされるかどうか。 特定の詳細のプロセッサのマニュアルを参照してください。 特定の 1 つのインスタンスにアクセスされる範囲がブレークポイントの範囲と重複するたびに、プロセッサ、読み取りまたは書き込みのブレークポイントがトリガーされる、x86 ことができます。

同様に場合、 **e** (execute) 0x00401003、アドレスにブレークポイントが設定し、2 バイトの命令またがりメモリ割り当て、アドレス 0x00401002 および 0x00401003 の実行、結果はプロセッサに依存します。 ここでも、詳細については、プロセッサ アーキテクチャのマニュアルを参照してください。

プロセッサは、ユーザー モード デバッガーによって設定されたブレークポイントとカーネル モード デバッガーによって設定されたブレークポイントによって区別されます。 ユーザー モードのプロセッサ ブレークポイントは、カーネル モード プロセスには影響しません。 カーネル モード プロセッサ ブレークポイント、可能性がありますまたは可能性がありますされませんユーザー モード プロセスに影響を与えるユーザー モード コードは、デバッグを使用しているかどうかに応じて状態を登録し、ユーザー モード デバッガーがアタッチされているかどうか。

現在のプロセスの既存のデータ ブレークポイントを別のレジスタのコンテキストに適用するには、使用、 [ **.apply\_dbp (適用データ ブレークポイントのコンテキストに)** ](-apply-dbp--apply-data-breakpoint-to-context-.md)コマンド。

マルチプロセッサ コンピューターでは、各プロセッサのブレークポイントは、すべてのプロセッサに適用されます。 たとえば、コマンドを使用すると、現在のプロセッサが 3 `ba e1 MyAddress` MyAddress、いずれかのプロセッサにブレークポイントを配置するだけでなく 3: を実行するプロセッサでは、そのアドレスにブレークポイントをトリガーします。 (これは、ソフトウェア ブレークポイントもします。)

のみ異なる同じアドレスで複数のプロセッサのブレークポイントを作成することはできません、*クラスヒント*値。 さまざまな制限が同じアドレスで複数のブレークポイントを作成できます (たとえば、異なる値の **/p**、 **/t**、 **/c**、および **/C**オプション)。

プロセッサのブレークポイントとそれらに適用される追加の制限の詳細については、次を参照してください。[プロセッサ ブレークポイント (ba ブレークポイント)](processor-breakpoints---ba-breakpoints-.md)します。

次の例に示す、 **ba**コマンド。 次のコマンドは、変数の myVar の 4 バイトの読み取りアクセス用のブレークポイントを設定します。

```dbgcmd
0:000> ba r4 myVar
```

次のコマンドは、0x3F8 0x3FB を通じてからアドレスを持つすべてのシリアル ポートにブレークポイントを追加します。 何もの読み取りまたはこれらのポートに書き込まれた場合は、このブレークポイントがトリガーされます。

```dbgcmd
kd> ba i4 3f8
```

 

 





