---
title: 擬似レジスタ構文
description: 擬似レジスタ構文
ms.assetid: f7dc52ea-e97e-4251-a517-c115cbc7d056
keywords:
- 擬似レジスタ
- pseudo-registers, automatic
- ユーザー定義の擬似レジスタ
- レジスタ、擬似レジスタ
- ループ変数
- アドレスを返す
- $t19 擬似レジスタに $
- $bp ID の擬似レジスタ
- $ea
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d459b99d76a14123a6a407d69a271822451f52b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528774"
---
# <a name="pseudo-register-syntax"></a>擬似レジスタ構文


## <span id="ddk_pseudo_register_syntax_dbg"></span><span id="DDK_PSEUDO_REGISTER_SYNTAX_DBG"></span>


デバッガーでは、特定の値を保持するいくつかの擬似レジスタをサポートします。

デバッガー セット*自動の擬似レジスタ*役に立つ特定の値にします。 *ユーザー定義の擬似レジスタ*への書き込みまたは読み取り可能な整数変数です。

すべての擬似レジスタがドル記号で始まる (**$**)。 追加できます MASM 構文を使用しているかどうか、アット マーク ( **@** )、ドル記号の前にします。 デバッガーを指示このアット マークと、次のトークンは、レジスタまたは擬似レジスタ、シンボルではありません。 省略した場合、アット マークは、デバッガーは応答速度が遅く、全体のシンボル テーブルを検索する必要があるためです。

たとえば、次の 2 つのコマンドは、同じ出力を生成しますが、2 番目のコマンドは、高速です。

```dbgcmd
0:000> ? $exp
Evaluate expression: 143 = 0000008f
0:000> ? @$exp
Evaluate expression: 143 = 0000008f
```

かどうかは、擬似レジスタと同じ名前のシンボルが存在する、追加する必要あります、アット マークします。

C++ の式の構文を使用している場合、アット マーク ( **@** ) が常に必要です。

[ **R (レジスタ)** ](r--registers-.md)コマンドは、この規則の例外。 デバッガーは常に登録または擬似レジスタとして、最初の引数を解釈します。 (にサインインのために必要なまたは許可されていない)。2 番目の引数がある場合、 **r**コマンドで、既定の式の構文に従って解釈されます。 既定式の構文が C++ の場合は、コピーする次のコマンドを使用する必要があります、 **$t2**擬似レジスタを **$t1**擬似レジスタ。

```dbgcmd
0:000> r $t1 = @$t2
```

### <a name="span-idautomaticpseudoregistersspanspan-idautomaticpseudoregistersspanautomatic-pseudo-registers"></a><span id="automatic_pseudo_registers"></span><span id="AUTOMATIC_PSEUDO_REGISTERS"></span>自動の擬似レジスタ

デバッガーは、次の擬似レジスタを自動的に設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">擬似レジスタ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>$ea</strong></p></td>
<td align="left"><p>実行された最後の命令の有効なアドレス。 この命令には有効なアドレスがあるない場合、デバッガーが表示されます&quot;不適切な登録エラー&quot;します。 この命令は、2 つの有効なアドレスを持っている場合、デバッガーには、最初のアドレスが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ea2</strong></p></td>
<td align="left"><p>実行された最後の命令の 2 番目の有効なアドレス。 デバッガーを表示する場合はこの命令には、2 つの有効なアドレスがあるない、&quot;不適切な登録エラー&quot;します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exp</strong></p></td>
<td align="left"><p>評価された最後の式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ra</strong></p></td>
<td align="left"><p>現在、スタック上にあるリターン アドレス。</p>
<p>このアドレスは、コマンドの実行で特に便利です。 たとえば、 <strong>g @$ ra</strong>リターン アドレスが見つかるまで続けられます (が<strong><a href="gu--go-up-.md" data-raw-source="[gu (Go Up)](gu--go-up-.md)">gu (Go Up)</a></strong>効果的な方法がより正確なの&quot;ステップ アウト&quot;、現在の関数)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ip</strong></p></td>
<td align="left"><p>命令ポインター レジスタ。</p>
<p></p>
<strong>x86 プロセッサ:</strong>同じ<strong>eip</strong>します。
<strong>Itanium ベースのプロセッサの場合:</strong>関連する<strong>iip</strong>します。 (詳細については、次の表の次の注を参照してください)。<strong>x64 ベース プロセッサ。</strong>同じ<strong>rip</strong>します。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$eventip</strong></p></td>
<td align="left"><p>現在のイベントの時点で命令ポインター。 このポインターは通常と一致する<strong>$ip</strong>スレッドを切り替えるか、命令ポインターの値を手動で変更しない限り、します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$previp</strong></p></td>
<td align="left"><p>前のイベントの時点で、命令ポインター。 (デバッガーの中断イベントとしてカウント)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$relip</strong></p></td>
<td align="left"><p>現在のイベントに関連する命令ポインター。 ブランチのトレースが、このポインターは、ブランチ ソースへのポインターになります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$scopeip</strong></p></td>
<td align="left"><p>現在の命令ポインター<a href="changing-contexts.md#local-context" data-raw-source="[local context](changing-contexts.md#local-context)">ローカル コンテキスト</a>(とも呼ばれる、<em>スコープ</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exentry</strong></p></td>
<td align="left"><p>現在のプロセスの最初の実行可能ファイルのエントリ ポイントのアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$retreg</strong></p></td>
<td align="left"><p>プライマリの戻り値レジスタです。</p>
<p></p>
<strong>x86 プロセッサ:</strong>同じ<strong>eax</strong>します。
<strong>Itanium ベースのプロセッサの場合:</strong>同じ<strong>ret0</strong>します。
<strong>x64 ベース プロセッサ。</strong>同じ<strong>rax</strong>します。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$retreg64</strong></p></td>
<td align="left"><p>プライマリの戻り値は、64 ビット形式で登録します。</p>
<p><strong>x86 プロセッサ。</strong>同じ、 <strong>edx:eax</strong>ペア。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$csp</strong></p></td>
<td align="left"><p>現在のコール スタック ポインター。 このポインターは、呼び出しスタックの深さのほとんどの代表的なレジスタです。</p>
<p></p>
<strong>x86 プロセッサ:</strong>同じ<strong>esp</strong>します。<strong>Itanium ベースのプロセッサの場合:</strong>同じ<strong>bsp</strong>します。
<strong>x64 ベース プロセッサ。</strong>同じ<strong>rsp</strong>します。</td>
</tr>
<tr class="even">
<td align="left"><p><strong>$p</strong></p></td>
<td align="left"><p>値を最終<strong><a href="d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md" data-raw-source="[d* (Display Memory)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)">d * (ディスプレイ メモリ)</a></strong>印刷コマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$proc</strong></p></td>
<td align="left"><p>現在のプロセス (つまり、」プロセス ブロックのアドレス) のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$thread</strong></p></td>
<td align="left"><p>現在のスレッドのアドレス。 カーネル モードのデバッグでは、このアドレスは、ETHREAD ブロックのアドレスです。 ユーザー モードのデバッグでは、このアドレスは、終了スレッド環境ブロックのアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$peb</strong></p></td>
<td align="left"><p>現在のプロセスのプロセスの環境ブロック (PEB) のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$teb</strong></p></td>
<td align="left"><p>現在のスレッドの終了スレッド環境ブロックのアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$tpid</strong></p></td>
<td align="left"><p>現在のスレッドを所有するプロセスのプロセス ID (PID)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$tid</strong></p></td>
<td align="left"><p>現在のスレッドのスレッド ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$dtid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$dpid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$dsid</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bp</strong><em>Number</em></p></td>
<td align="left"><p>対応するブレークポイントのアドレス。 たとえば、<strong>ドル bp3</strong> (または<strong>ドル bp03</strong>) ブレークポイント ID が 3 のブレークポイントを参照します。 <em>数</em>は常に 10 進数。 ブレークポイントの ID を持たない場合<em>数</em>、 <strong>$bp</strong><em>数</em>0 に評価します。 ブレークポイントの詳細については、次を参照してください。<a href="using-breakpoints.md" data-raw-source="[Using Breakpoints](using-breakpoints.md)">を使用してブレークポイント</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$frame</strong></p></td>
<td align="left"><p>現在のフレーム インデックス。 このインデックスは、同じフレーム番号、 <strong><a href="-frame--set-local-context-.md" data-raw-source="[.frame (Set Local Context)](-frame--set-local-context-.md)">.frame (ローカル コンテキストの設定)</a></strong>コマンドで使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$dbgtime</strong></p></td>
<td align="left"><p>デバッガーが実行されているコンピューターに準じた現在時刻。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$callret</strong></p></td>
<td align="left"><p>関数の戻り値、最後の<strong><a href="-call--call-function-.md" data-raw-source="[.call (Call Function)](-call--call-function-.md)">.call (関数の呼び出し)</a></strong>呼び出されるかで使用されている、 <strong><a href="-fnret--display-function-return-value-.md" data-raw-source="[.fnret /s](-fnret--display-function-return-value-.md)">.fnret/s</a></strong>コマンド。 データ型<strong>$callret</strong>この戻り値のデータ型です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$extret</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$extin</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$clrex</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$lastclrex</strong></p></td>
<td align="left"><p><strong>マネージ デバッグのみ。</strong>共通言語ランタイム (CLR) 例外の最後に発生したオブジェクトのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ptrsize</strong></p></td>
<td align="left"><p>ポインターのサイズ。 カーネル モードでは、このサイズは、ターゲット コンピューターのポインター サイズです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pagesize</strong></p></td>
<td align="left"><p>メモリの 1 つのページのバイト数。 カーネル モードでは、このサイズは、ターゲット コンピューターのページ サイズです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$pcr</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$pcrb</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$argreg</strong></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ exr_chance</strong></p></td>
<td align="left"><p>現在の例外レコードのチャンスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$ exr_code</strong></p></td>
<td align="left"><p>例外レコードの現在の例外コード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$ exr_numparams</strong></p></td>
<td align="left"><p>現在の例外レコード内のパラメーターの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param0 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 0 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>exr_param1 ドル</strong></p></td>
<td align="left"><p>現在の例外レコードのパラメーター 1 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$exr_param2</strong></p></td>
<td align="left"><p>現在の例外レコードでパラメーター 2 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param3</strong></p></td>
<td align="left"><p>現在の例外レコードでパラメーター 3 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param4 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 4 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>exr_param5 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 5 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param6 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 6 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param7</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 7 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param8 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 8 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>exr_param9 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 9 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param10 ドル</strong></p></td>
<td align="left"><p>現在の例外レコードのパラメーターの 10 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param11</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 11 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param12 ドル</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 12 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$exr_param13</strong></p></td>
<td align="left"><p>現在の例外レコード パラメーター 13 の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>exr_param14 ドル</strong></p></td>
<td align="left"><p>現在の例外レコードのパラメーターの 14 の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_code</strong></p></td>
<td align="left"><p>バグ チェックが発生した場合は、バグ コードになります。 カーネル モードのデバッグとカーネル クラッシュ ダンプをライブに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug_param1</strong></p></td>
<td align="left"><p>バグ チェックが発生した場合は、パラメーター 1 の値になります。 カーネル モードのデバッグとカーネル クラッシュ ダンプをライブに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_param2</strong></p></td>
<td align="left"><p>バグ チェックが発生した場合は、パラメーター 2 の値になります。 カーネル モードのデバッグとカーネル クラッシュ ダンプをライブに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>$bug_param3</strong></p></td>
<td align="left"><p>バグ チェックが発生した場合は、パラメーター 3 の値になります。 カーネル モードのデバッグとカーネル クラッシュ ダンプをライブに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>$bug_param4</strong></p></td>
<td align="left"><p>バグ チェックが発生した場合は、パラメーター 4 の値になります。 カーネル モードのデバッグとカーネル クラッシュ ダンプをライブに適用されます。</p></td>
</tr>
</tbody>
</table>

 

これらの擬似レジスタの一部は特定のデバッグ シナリオで使用できません。 たとえば、使用することはできません **$peb**、 **$tid**、および **$tpid**ユーザー モードのミニダンプまたは特定のカーネル モードのダンプ ファイルをデバッグする際にします。 スレッドからの情報を確認する場合があります[ **~ (スレッド ステータス)** ](---thread-status-.md)がからではなく **$tid**します。 使用することはできません、 **$previp**デバッガーの最初のイベントの擬似レジスタ。 使用することはできません、 **$relip**擬似レジスタ ブランチ トレースがないです。 利用不可の擬似レジスタを使用する場合は、構文エラーが発生します。

など、構造体は--のアドレスを保持する擬似レジスタ **$thread**、 **$proc**、 **$teb**、 **$peb**、および **$lastclrex** -MASM 式エバリュエーターではなく、C++ の式エバリュエーターでは、適切なデータ型に従って評価されます。 たとえば、次のコマンド**でしょうか。 $teb**コマンドの中に、TEB のアドレスが表示されます **?? @$ teb** TEB 構造全体が表示されます。 詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)します。

Itanium ベースのプロセッサでは、上、 **iip**レジスタ*バンドル揃え*、別のスロットが実行されている場合でも、現在の命令を含む、バンドルに 0 をスロットを指すことを意味します。 したがって**iip**は完全な命令ポインターではありません。 **$Ip**擬似レジスタは、バンドル、スロットなど、実際の命令ポインター。 アドレスのポインターを保持する他の擬似レジスタ (**$ra**、 **$retreg**、 **$eventip**、 **$previp**、 **$relip**、および **$exentry**) と同じ構造がある **$ip**すべてのプロセッサでします。

使用することができます、 **r**の値を変更するコマンド **$ip**します。 この変更は、対応するレジスタも自動的に変更します。 実行が再開されると、新しい命令ポインター アドレスで再開します。 この登録は、手動で変更することができますのみ自動の擬似レジスタです。

**注**  で MASM の構文に示すことができます、 **$ip**擬似レジスタにピリオド (**します。** ). 追加しないでください、アット マーク (@)、この期間より前に、の最初のパラメーターとして、期間を使用しないと、 **r**コマンド。 この構文は C++ の式内で許可されていません。

 

自動の擬似レジスタはのような[自動エイリアス](using-aliases.md)します。 エイリアスに関連したトークンと共に自動のエイリアスを使用することができますが、(など **$ {}**)、このようなトークンで擬似レジスタを使用することはできません。

### <a name="span-iduserdefinedpseudoregistersspanspan-iduserdefinedpseudoregistersspanuser-defined-pseudo-registers"></a><span id="user_defined_pseudo_registers"></span><span id="USER_DEFINED_PSEUDO_REGISTERS"></span>ユーザー定義の擬似レジスタ

20 ユーザー定義の擬似レジスタがある (**$t0**、 **$t1**,...,**ドル t19**)。 これらの擬似レジスタは、デバッガーを使用して書き込みおよび読み取りできる変数です。 これらの擬似レジスタには、任意の整数値を格納できます。 ループ変数として特に役に立ちます。

これらの擬似レジスタのいずれかに書き込むを使用して、 [ **r (レジスタ)** ](r--registers-.md)コマンドを次の例を示します。

```dbgcmd
0:000> r $t0 = 7
0:000> r $t1 = 128*poi(MyVar)
```

すべての擬似レジスタのように、次の例として、任意の式で、ユーザー定義の擬似レジスタを使用できます。

```dbgcmd
0:000> bp $t3 
0:000> bp @$t4 
0:000> ?? @$t1 + 4*@$t2 
```

使用しない限り、擬似レジスタが整数として型指定された常に、**でしょうか。** スイッチと組み合わせて、 **r**コマンド。 このスイッチを使用する場合、擬似レジスタは、それに割り当てられている任意の種類を取得します。 たとえば、次のコマンドは、UNICODE を割り当てられます。\_文字列\*\*型とする 0x0012FFBC 値**ドル t15**します。

```dbgcmd
0:000> r? $t15 = * (UNICODE_STRING*) 0x12ffbc
```

ユーザー定義の擬似レジスタは、デバッガーが開始されると、既定値として 0 を使用します。

**注**  エイリアス**ドル u0**、 **$u1**,...,**ドル u9**のような外観に関係なく、擬似レジスタではありません。 これらの別名の詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

 

### <a name="span-idexample1spanspan-idexample1spanexample"></a><span id="example1"></span><span id="EXAMPLE1"></span>例

次の例では、現在のスレッドを呼び出すたびにヒットするブレークポイントを設定する**NtOpenFile**します。 その他のスレッドの呼び出し時に、このブレークポイントがヒットしないが、 **NtOpenFile**します。

```dbgcmd
kd> bp /t @$thread nt!ntopenfile
```

### <a name="span-idexample2spanspan-idexample2spanexample"></a><span id="example2"></span><span id="EXAMPLE2"></span>例

次の例は、レジスタが指定された値を保持するまでのコマンドを実行します。 まず、"eaxstep"をという名前のスクリプト ファイルで条件付きステップを実行するための次のコードを配置します。

```dbgcmd
.if (@eax == 1234) { .echo 1234 } .else { t "$<eaxstep" }
```

次に、次のコマンドを発行します。

```dbgcmd
t "$<eaxstep"
```

デバッガーでは、ステップを実行しから、コマンドを実行します。 デバッガーがいずれかが表示されるスクリプトを実行するこの例では、 **1234**またはプロセスを繰り返します。

 

 





