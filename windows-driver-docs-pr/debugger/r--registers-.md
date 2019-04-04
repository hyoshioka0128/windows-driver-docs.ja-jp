---
title: r (レジスタ)
description: R コマンドを表示またはレジスタ、浮動小数点レジスタ、フラグ、擬似レジスタ、および固定名のエイリアスを変更します。
ms.assetid: c0d0af2f-1852-47a4-8f01-95f6ec198112
keywords:
- r (レジスタ) Windows のデバッグ
ms.date: 07/11/2018
topic_type:
- apiref
api_name:
- r (Registers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c66fd4bb9650e9e26eb6e4a5d0aeff86da6c949
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579253"
---
# <a name="r-registers"></a>r (レジスタ)


**R**コマンドが表示またはレジスタ、浮動小数点レジスタ、フラグ、擬似レジスタ、および固定名のエイリアスを変更します。

ユーザー モード

```dbgcmd
[~Thread] r[M Mask|F|X|?] [ Register[:[Num]Type] [= [Value]] ] 
r.
```

カーネル モード

```dbgcmd
[Processor] r[M Mask|F|X|Y|YI|?] [ Register[:[Num]Type] [= [Value]] ] 
r.
```

## <a name="span-idddkcmdregistersdbgspanspan-idddkcmdregistersdbgspanparameters"></a><span id="ddk_cmd_registers_dbg"></span><span id="DDK_CMD_REGISTERS_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサのレジスタが読み取り元を指定します。 既定値は 0 です。 指定した場合*プロセッサ*、含めることはできません、*登録*パラメーター--すべてのレジスタが表示されます。 構文の詳細については、[マルチプロセッサ構文](multiprocessor-syntax.md)を参照してください。 プロセッサは、カーネル モードでのみ指定できます。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
レジスタが読み取られるスレッドを指定します。 スレッドを指定しない場合は、現在のスレッドが使用されます。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______M_______Mask______"></span><span id="_______m_______mask______"></span><span id="_______M_______MASK______"></span> **M** *マスク*   
デバッガー、レジスタを表示するときに使用するマスクを指定します。 "M"は大文字である必要があります。 *マスク*はレジスタの表示について何かを示すビットの合計です。 ビットの意味は、プロセッサと、モードによって異なります (詳細については、次の「解説」表を参照してください)。 省略した場合**M**既定のマスクを使用します。 設定またはを使用して既定のマスクを表示することができます、 [ **Rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______F______"></span><span id="_______f______"></span> **F**   
浮動小数点レジスタが表示されます。 "F"は大文字である必要があります。 このオプションに相当**M 0x4**します。

<span id="_______X______"></span><span id="_______x______"></span> **X**   
SSE の XMM レジスタを表示します。 このオプションに相当**M 0x40**します。

<span id="_______Y______"></span><span id="_______y______"></span> **Y**   
AVX YMM レジスタが表示されます。 このオプションに相当**M 0x200**します。

<span id="_______YI______"></span><span id="_______yi______"></span> **YI**   
整数レジスタ AVX YMM が表示されます。 このオプションに相当**M 0x400**します。

<span id="_______YI______"></span><span id="_______yi______"></span> **Z**   
浮動小数点形式で avx-512 YMM レジスタ (zmm0 zmm31) を表示します。 

<span id="_______YI______"></span><span id="_______yi______"></span> **ZI**   
整数形式で avx-512 YMM レジスタ (zmm0 zmm31) が表示されます。 

<span id="_______YI______"></span><span id="_______yi______"></span> **K**   
Avx-512 Opmask 述語レジスタ (K0 K7) を表示します。

<span id="______________"></span> **?**   
(擬似レジスタ割り当てのみ)型指定された情報を取得する擬似レジスタをによりします。 任意の型が許可されます。 詳細については、 **r?** 構文を参照してください[デバッガー コマンド プログラム例](debugger-command-program-examples.md)します。

<span id="_______Register______"></span><span id="_______register______"></span><span id="_______REGISTER______"></span> *登録*   
登録、フラグ、擬似レジスタ、または表示または変更する固定名のエイリアスを指定します。 このパラメーターにする前にする必要があります (**@**) 記号です。 構文の詳細については、[登録構文](register-syntax.md)を参照してください。

<span id="_______Num______"></span><span id="_______num______"></span><span id="_______NUM______"></span> *num*   
表示する要素の数を指定します。 含めることはこのパラメーターを省略した場合*型*、完全な登録の長さが表示されます。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
内の各レジスタ要素を表示するデータ形式を指定します。 使用することができます*型*64 ビットおよび 128 ビット ベクター レジスタでのみです。 複数の種類を指定することができます。

次の値の 1 つ以上を指定することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>型</em></th>
<th align="left">表示形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>ib</strong></p></td>
<td align="left"><p>符号付きバイト</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ub</strong></p></td>
<td align="left"><p>符号なしバイト</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iw</strong></p></td>
<td align="left"><p>符号付きの単語</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uw</strong></p></td>
<td align="left"><p>符号なし単語</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>id</strong></p></td>
<td align="left"><p>符号付き DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ud</strong></p></td>
<td align="left"><p>符号なしの DWORD</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>iq</strong></p></td>
<td align="left"><p>符号付きクワドワード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>uq</strong></p></td>
<td align="left"><p>符号なしのクワドワード</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>f</strong></p></td>
<td align="left"><p>32 ビット浮動小数点</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>64 ビット浮動小数点</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
レジスタに割り当てる値を指定します。 構文の詳細については、[数値式の構文](numerical-expression-syntax.md)を参照してください。

 **.**   
現在の命令で使用されるレジスタを表示します。 レジスタが使用されていない場合、出力は表示されません。

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

レジスタのコンテキストとその他のコンテキストの設定の詳細については、[変更コンテキスト](changing-contexts.md)を参照してください。

<a name="remarks"></a>コメント
-------

指定しない場合*登録*、 **r**コマンドでは、すべての非浮動小数点レジスタを表示します。 および**rF**コマンドは、すべての浮動小数点レジスタを表示します。 使用してこの動作を変更することができます、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

指定した場合*登録*ですが、等号 (=) は省略、*値*コマンドのパラメーターがレジスタの現在の値が表示されます。

指定した場合*登録*が等号 (=) を省略し、*値*コマンドは、レジスタの現在の値を表示し、新しい値を要求します。

指定した場合*登録*、等号 (=)、および*値*コマンドは、値を格納するレジスタを変更します。 (場合*quiet モード*がアクティブでは省略できます等号 (=)。 Quiet モードをオンするを使用して、 [ **sq (非表示モードの設定)** ](sq--set-quiet-mode-.md)コマンド。 カーネル モードでにすることも非表示モードで、KDQUIET を使用して[環境変数](kernel-mode-environment-variables.md))。

コンマで区切られた複数のレジスタを指定することができます。

ユーザー モードで、 **r**コマンドには、現在のスレッドに関連付けられているレジスタが表示されます。 スレッドの詳細については、[を制御するプロセスとスレッド](controlling-processes-and-threads.md)を参照してください。

カーネル モードで、 **r**コマンドには、現在に関連付けられているレジスタが表示されます。*コンテキストを登録*します。 特定のスレッド、コンテキストのレコードを一致するように登録するコンテキストを設定したり、フレームをトラップします。 指定されたレジスタのコンテキストの最も重要なレジスタのみが実際に表示される、およびその値を変更することはできません。 レジスタのコンテキストの詳細については、[登録コンテキスト](changing-contexts.md#register-context)を参照してください。

名前で、浮動小数点レジスタを指定すると、 **F**オプションは必要ありません。 1 つの浮動小数点レジスタを指定すると、10 進数の値だけでなく、生の 16 進数の値が表示されます。

次*マスク*x86 ベースのプロセッサまたは x64 ベースのプロセッサのビットがサポートされています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
0 1</td>
<td align="left"><p></p>
0x1 0x2</td>
<td align="left"><p>基本整数レジスタを表示します。 (これらのビットの一方または両方を設定するのと同じ効果です。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0x4</p></td>
<td align="left"><p>浮動小数点レジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>セグメントのレジスタが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>MMX レジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>5</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>デバッグのレジスタが表示されます。 カーネル モードでこのビットを設定も表示されます、CR4 レジスタ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>6</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>SSE の XMM レジスタを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>(カーネル モードのみ)CR0、CR2、CR3 および CR8 などの制御レジスタが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>0x100</p></td>
<td align="left"><p>(カーネル モードのみ)記述子およびタスクの状態のレジスタが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"><p>AVX YMM を浮動小数点の登録を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>0x400</p></td>
<td align="left"><p>AVX YMM を 10 進整数で登録を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>11</p></td>
<td align="left"><p>0x800</p></td>
<td align="left"><p>10 進整数での AVX XMM レジスタを表示します。</p></td>
</tr>
</tbody>
</table>


 

次のコード例に示す**r** x86 ベースのプロセッサ用のコマンド。

カーネル モードでは、次のコマンドは、2 プロセッサのレジスタを示します。

```dbgcmd
1: kd> 2r 
```

ユーザー モードでは、次のコマンドは、スレッド 2 のレジスタを示します。

```dbgcmd
0:000> ~2 r 
```

次のコマンドでは、ユーザー モードで表示のすべて、 **eax** (スレッドのインデックス順序) のすべてのスレッドに関連付けられている登録します。

```dbgcmd
0:000> ~* r eax
```

次のコマンド セット、 **eax** 0x000000FF に現在のスレッドに登録します。

```dbgcmd
0:000> r eax=0x000000FF
```

次のコマンド セット、 **st0 を割り当てます**1.234e + 10 に登録 (、 **F**は省略可能)。

```dbgcmd
0:000> rF st0=1.234e+10
```

次のコマンドは、0 フラグを表示します。

```dbgcmd
0:000> r zf 
```

次のコマンドが表示されます、 **xmm0** 16 の符号なしバイトとして登録しの完全な内容を表示、 **xmm1**倍精度浮動小数点形式で登録します。

```dbgcmd
0:000> r xmm0:16ub, xmm1:d 
```

現在の構文が C++ の場合は、レジスタで前に指定する必要があります、アット マーク (**@**)。 そのため、次のコマンドを使用してコピーする可能性があります、 **ebx**を登録、 **eax**を登録します。

```dbgcmd
0:000> r eax = @ebx
```

次のコマンドと同じで擬似レジスタを表示する方法、 **r**コマンドには、レジスタが表示されます。

```dbgcmd
0:000> r $teb
```

使用することも、 **r**を作成するコマンド*固定名のエイリアス*します。 これらのエイリアスはいないレジスタまたは擬似レジスタに関連付けられている場合でも、 **r**コマンド。 これらの別名の詳細については、[Using エイリアス](using-aliases.md)を参照してください。

次の例に示します、 **r です。** x86 ベースのプロセッサにコマンド。 呼び出し履歴の最後のエントリには、コマンド自体が先頭に付きます。

```dbgcmd
01004af3 8bec            mov     ebp,esp
0:000> r.
ebp=0006ffc0  esp=0006ff7c
```


 

 





