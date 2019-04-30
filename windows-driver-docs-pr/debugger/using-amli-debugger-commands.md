---
title: AMLI Debugger コマンドの使用
description: AMLI Debugger コマンドの使用
ms.assetid: 8efa6f13-67db-417a-83ec-8219afc9874c
keywords:
- AMLI デバッガー、AMLI デバッガー コマンド
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e6507ad0e708e59444f229a9df8489272e9dce0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383746"
---
# <a name="using-amli-debugger-commands"></a>AMLI Debugger コマンドの使用


## <span id="ddk_using_amli_debugger_commands_dbg"></span><span id="DDK_USING_AMLI_DEBUGGER_COMMANDS_DBG"></span>


AMLI デバッガー プロンプトから次のコマンドを発行できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[全般] カテゴリ</th>
<th align="left">特定のアクション</th>
<th align="left">AMLI デバッガー コマンド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバッガーの制御</p></td>
<td align="left"><p></p>
カーネル デバッガーの実行の中断を続行します。</td>
<td align="left"><p></p>
<strong>g</strong>
<strong>q</strong></td>
</tr>
<tr class="even">
<td align="left"><p>AML 実行を制御します。</p></td>
<td align="left"><p></p>
AML コードのトレースを AML コードにメソッドのステップを実行します。</td>
<td align="left"><p></p>
<strong>run</strong>
<strong>p</strong>
<strong>t</strong></td>
</tr>
<tr class="odd">
<td align="left"><p>トレース モードの設定を制御します。</p></td>
<td align="left"><p>トレース モードを構成します。</p></td>
<td align="left"><p><strong>トレース</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>Namespace オブジェクトへの通知</p></td>
<td align="left"><p>Namespace オブジェクトへの通知します。</p></td>
<td align="left"><p><strong>notify</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>オブジェクトの数のテーブルを表示します。</p></td>
<td align="left"><p>表示オブジェクト カウント テーブル</p></td>
<td align="left"><p><strong>dc</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>メモリへのアクセス</p></td>
<td align="left"><p></p>
表示データの表示データ バイト表示データ単語表示データ Dword 表示データ文字列編集メモリ</td>
<td align="left"><p></p>
<strong>d</strong>
<strong>db</strong>
<strong>dw</strong>
<strong>dd</strong>
<strong>da</strong>
<strong>e</strong></td>
</tr>
<tr class="odd">
<td align="left"><p>ポートへのアクセス</p></td>
<td align="left"><p></p>
ポートからポート読み取り Word からの読み取りバイトを読み取る DWORD ポートからをポート書き込み Word ポート書き込みポートを DWORD にバイトを書き込む</td>
<td align="left"><p></p>
<strong></strong>
<strong>iw</strong>
<strong>id</strong>
<strong>o</strong>
<strong>ow</strong>
<strong>od</strong></td>
</tr>
<tr class="even">
<td align="left"><p>ヘルプの表示</p></td>
<td align="left"><p>ヘルプを表示します。</p></td>
<td align="left"><p><strong>?</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcontrollingthedebuggerspanspan-idcontrollingthedebuggerspancontrolling-the-debugger"></a><span id="controlling_the_debugger"></span><span id="CONTROLLING_THE_DEBUGGER"></span>デバッガーの制御

これらのコマンドは、AMLI デバッガーを終了します。 **G**コマンドは、対象のコンピューターの正常な実行を再開し、 **q**コマンドは、対象のコンピュータを固定およびカーネル デバッガーを中断します。

**g**

**q**

### <a name="span-idcontrollingamlexecutionspanspan-idcontrollingamlexecutionspancontrolling-aml-execution"></a><span id="controlling_aml_execution"></span><span id="CONTROLLING_AML_EXECUTION"></span>AML 実行を制御します。

これらのコマンドを使用すると、AML メソッドをステップまたは実行できます。 **実行**コマンドは、特定の時点での実行を開始します。 **P**と**t**コマンドでは、ステップ、一度に 1 つの命令を実行できます。 関数呼び出しが発生した場合、 **p**コマンドは、1 つの手順として、関数を処理中に、 **t**トレースを新しい関数に、一度に 1 つ命令にコマンドします。


**実行** *MethodName*  **\[ ***ArgumentList***\]**

**実行** *CodeAddress*  **\[ ***ArgumentList***\]**

**p**

**t**

<span id="MethodName"></span><span id="methodname"></span><span id="METHODNAME"></span>*methodName*  
メソッドの名前と完全なパスを指定します。 このメソッドのメモリ位置の先頭に、実行が開始されます。

<span id="CodeAddress"></span><span id="codeaddress"></span><span id="CODEADDRESS"></span>*CodeAddress*  
実行の開始アドレスを指定します。

<span id="ArgumentList"></span><span id="argumentlist"></span><span id="ARGUMENTLIST"></span>*ArgumentList*  
メソッドに渡される引数のリストを指定します。 各引数は整数である必要があります。 複数の引数は、スペースで区切る必要があります。

### <a name="span-idcontrollingtracemodesettingsspanspan-idcontrollingtracemodesettingsspancontrolling-trace-mode-settings"></a><span id="controlling_trace_mode_settings"></span><span id="CONTROLLING_TRACE_MODE_SETTINGS"></span>トレース モードの設定を制御します。

**トレース**コマンドは、AML インタープリターのトレース モードの設定を制御します。 パラメーターなしでこのコマンドを使用する場合は、現在のトレース モードの設定が表示されます。

**トレース\[trigon | trigoff\] \[level =**<em>レベル</em> **\] \[追加 =**<em>TPStrings</em> **\] \[zap =**<em>TPNumbers</em>**\]**

<span id="trigon"></span><span id="TRIGON"></span>**trigon**  
トリガーのトレース モードをアクティブにします。

<span id="trigoff"></span><span id="TRIGOFF"></span>**trigoff**  
トリガーのトレース モードを無効になります。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>*レベル*  
トレース レベルの新しい設定を指定します。

<span id="TPStrings"></span><span id="tpstrings"></span><span id="TPSTRINGS"></span>*TPStrings*  
追加する 1 つまたは複数のトリガー ポイントを指定します。 各トリガー ポイントは、名前によって指定されます。 複数のトリガー ポイント文字列は、コンマで区切る必要があります。

<span id="TPNumbers"></span><span id="tpnumbers"></span><span id="TPNUMBERS"></span>*TPNumbers*  
削除する 1 つまたは複数のトリガー ポイントを指定します。 各トリガー ポイント数を指定します。 複数のトリガー ポイント番号をコンマで区切る必要があります。 小数点数のトリガーの一覧を表示する、**トレース**コマンドをパラメーターなし。

### <a name="span-idnotifyinganamespaceobjectspanspan-idnotifyinganamespaceobjectspannotifying-a-namespace-object"></a><span id="notifying_a_namespace_object"></span><span id="NOTIFYING_A_NAMESPACE_OBJECT"></span>Namespace オブジェクトへの通知

**通知**コマンドでは、ACPI 名前空間のオブジェクトに通知を送信します。 通知は、指定されたオブジェクトのキューに配置されます。

**notify** *ObjectName Value*

**通知** *ObjectAddress 値*

<span id="ObjectName"></span><span id="objectname"></span><span id="OBJECTNAME"></span>*ObjectName*  
通知を受けるオブジェクトの完全な名前空間パスを指定します。

<span id="ObjectAddress"></span><span id="objectaddress"></span><span id="OBJECTADDRESS"></span>*ObjectAddress*  
通知を受けるオブジェクトのアドレスを指定します。

<span id="Value"></span><span id="value"></span><span id="VALUE"></span>*値*  
通知の値を指定します。

### <a name="span-iddisplayingtheobjectcounttablespanspan-iddisplayingtheobjectcounttablespandisplaying-the-object-count-table"></a><span id="displaying_the_object_count_table"></span><span id="DISPLAYING_THE_OBJECT_COUNT_TABLE"></span>オブジェクトの数のテーブルを表示します。

**Dc**コマンドは、メモリ オブジェクトのカウント テーブルを表示します。

**dc**

### <a name="span-idaccessingmemoryspanspan-idaccessingmemoryspanaccessing-memory"></a><span id="accessing_memory"></span><span id="ACCESSING_MEMORY"></span>メモリへのアクセス

メモリのアクセス コマンドを使用すると、メモリを読み書きできます。 使用メモリ単位のサイズを選択するにはメモリを読み取るときに、 **db**、 **dw**、 **dd**または**da**コマンド。 単純な**d**コマンドは、最も最近に選択された単位でメモリを表示します。 これは、最初に使用される表示コマンドである場合は、バイト単位が使用されます。

アドレス、またはメソッドが指定されていない場合、前の表示コマンドが終了した位置の表示が開始されます。

これらのコマンドが、標準のカーネル デバッガー メモリ コマンドと同じ効果があります。これらは、アクセスしやすいように AMLI デバッガー内で複製されます。

**d\[b | w | d |、\] \[ \[l =**<em>長さ</em>**\] \[** *メソッド* **|  \[ %% \]**<em>アドレス</em> **\] \]**

**e \[ %% \]**  <em>Datalist アドレス</em>

<span id="b"></span><span id="B"></span>**B**  
データをバイト単位で表示することを指定します。

<span id="w"></span><span id="W"></span>**W**  
Word (16 ビット) 単位でデータを表示することを指定します。

<span id="d"></span><span id="D"></span>**D**  
DWORD (32 ビット) 単位でデータを表示することを指定します。

<span id="a"></span><span id="A"></span>**A**  
文字列としてデータを表示する必要がありますを指定します。 データは、ASCII 文字として表示されます。 NULL 文字が読み取られるとき、または表示を終了します*長さ*文字が表示されています。

<span id="Length"></span><span id="length"></span><span id="LENGTH"></span>*長さ*  
表示するバイト数を指定します。 *長さ*16 進数である必要があります (なし、 **0 x**プレフィックス)。 場合*長さ*は省略すると、既定の表示サイズが 0x80 バイト。

<span id="Method"></span><span id="method"></span><span id="METHOD"></span>*メソッド*  
メソッドの名前と完全なパスを指定します。 このメソッドのメモリ位置の先頭に表示が開始されます。

<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*アドレス*  
読み取りまたは書き込みを開始する場所のメモリ アドレスを指定します。 アドレスの 2 つのパーセント記号が付いている場合 (**%%**)、物理アドレスとして解釈されます。 それ以外の場合、その仮想アドレスとして解釈されます。

<span id="DataList"></span><span id="datalist"></span><span id="DATALIST"></span>*DataList*  
メモリに書き込まれるデータを指定します。 リスト内の各項目は、16 進のバイトまたは文字列のいずれかにできます。 文字列を使用する場合は、引用符で囲む必要があります。 複数の項目は、スペースで区切る必要があります。

### <a name="span-idaccessingportsspanspan-idaccessingportsspanaccessing-ports"></a><span id="accessing_ports"></span><span id="ACCESSING_PORTS"></span>ポートへのアクセス

ポートのコマンドを使用すると、出力を送信したり、データ ポートからの入力を受信したりできます。 **は**と**o**コマンドは、1 つ (バイト単位) を転送、 **iw**と**ow**コマンドは、単語 (16 ビット) を転送し、 **id**と**od**コマンドは、DWORD (32 ビット) を転送します。

これらのコマンドが、標準のカーネル デバッガー ポート コマンドと同じ効果があります。これらは、アクセスしやすいように AMLI デバッガー内で複製されます。

**i** *ポート*

**iw** *ポート*

**id** *ポート*

**o** *Port* *DataForPort*

**ow** *Port* *DataForPort*

**od** *Port* *DataForPort*

<span id="Port"></span><span id="port"></span><span id="PORT"></span>*ポート*  
ポートへのアクセスのアドレスを指定します。 ポート サイズは、選択したコマンドと一致する必要があります。

<span id="DataForPort"></span><span id="dataforport"></span><span id="DATAFORPORT"></span>*DataForPort*  
ポートに書き込むデータを指定します。 このデータのサイズは、選択したコマンドと一致する必要があります。

### <a name="span-iddisplayinghelpspanspan-iddisplayinghelpspandisplaying-help"></a><span id="displaying_help"></span><span id="DISPLAYING_HELP"></span>ヘルプの表示

このコマンドは、AMLI デバッガー コマンドのヘルプ テキストを表示します。

 **ですか。\[**<em>コマンド</em>**\]**

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*コマンド*  
ヘルプを表示するためのコマンドを指定します。 これを省略すると、すべての AMLI デバッガー コマンドと AMLI デバッガー拡張機能の一覧が表示されます。

## <a name="see-also"></a>関連項目

[AMLI デバッガー](the-amli-debugger.md) 
