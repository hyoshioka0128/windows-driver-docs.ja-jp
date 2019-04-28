---
title: s (メモリの検索)
description: S コマンドは、特定のバイト パターンを検索するメモリ内で検索します。
ms.assetid: fdca07c3-95c8-46cf-8da1-07a5e6767f67
keywords:
- s (検索メモリ) の Windows デバッグ
ms.date: 02/21/2019
topic_type:
- apiref
api_name:
- s (Search Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25e1a5b4f3e2c222b1822cd59452122ef1762f68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382014"
---
# <a name="s-search-memory"></a>s (メモリの検索)


**S**コマンドのメモリを検索し、特定のバイト パターンを検索します。

このコマンドを混同しないでください、 [ **~ s (変更の現在のプロセッサ)**](-s--change-current-processor-.md)、 [ **~ (設定現在のスレッド) s**](-s--set-current-thread-.md)、 [ **| s (現在のプロセスのセット)**](-s--set-current-process-.md)、または[ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンド。

```dbgcmd
s [-[[Flags]Type]] Range Pattern 
s -[[Flags]]v Range Object 
s -[[Flags]]sa Range 
s -[[Flags]]su Range 
```

## <a name="span-idddkcmdsearchmemorydbgspanspan-idddkcmdsearchmemorydbgspanparameters"></a><span id="ddk_cmd_search_memory_dbg"></span><span id="DDK_CMD_SEARCH_MEMORY_DBG"></span>パラメーター


<span id="_______________Flags______________"></span><span id="_______________flags______________"></span><span id="_______________FLAGS______________"></span> **\[** *フラグ*\]   
1 つまたは複数の検索オプションを指定します。 各フラグは、1 つの文字です。 フラグを 1 つの組の角かっこで囲む必要があります (\[\])。 間を除く、角かっこの間にスペースを追加することはできません**n**または**l**とその引数。 指定する場合など、 **s**と**w**オプションを使用して、コマンド s -\[sw\]型の範囲のパターン。

次のフラグの 1 つ以上を指定できます。

<span id="s"></span><span id="S"></span>**s**  
すべての現在の検索の結果を保存します。 これらの結果を使用して、後で、検索を繰り返すことができます。

<span id="r"></span><span id="R"></span>**R**  
最後の保存された検索結果を現在の検索を制限します。 使用することはできません、 **s**と**r**を同じコマンドでフラグ。 使用すると**r**の値*範囲*は無視されますと、デバッガーを検索する前に保存されたヒットだけ**s**コマンド。

<span id="n_Hits"></span><span id="n_hits"></span><span id="N_HITS"></span>**n** *ヒット数*  
使用するときに保存するヒットの数を指定します、 **s**フラグ。 既定値は、1024 のヒット数です。 使用する場合**n**他のフラグと共に**n**後に、最後のフラグでなければなりません、*ヒット*引数。 間のスペース**n**と*ヒット*は省略可能でが角かっこ内の他のスペースを追加することはできません。 使用して後で検索する場合、 **s**フラグは、ヒット数の指定した数よりも多く検出、**オーバーフローしました。 エラー**にすべてのヒット数を保存していることを通知するメッセージが表示されます。

<span id="l_Length"></span><span id="l_length"></span><span id="L_LENGTH"></span>**l** *長さ*  
以上の文字列のみを返す任意の ASCII または Unicode 文字列の検索と*長さ*文字。 既定の長さは 3 です。 この値に影響を使用する唯一の検索、 **sa**または**su**フラグ。

<span id="w"></span><span id="W"></span>**W**  
書き込み可能なメモリの領域のみを検索します。 "W"は、角かっこで囲む必要があります。

<span id="1"></span>**1**  
検索の出力でと一致する検索のアドレスだけが表示されます。 このオプションを使用している場合に便利ですが、 [ **.foreach** ](-foreach.md)コマンドの出力を別のコマンドにパイプするためのトークンの入力します。

<span id="_______Type______"></span><span id="_______type______"></span><span id="_______TYPE______"></span> *型*   
検索するメモリの種類を指定します。 前のハイフン (-) を追加*型*します。 次のいずれかを使用することができます*型*値。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>b</strong></p></td>
<td align="left"><p>バイト (8 ビット)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>w</strong></p></td>
<td align="left"><p>WORD (16 ビット)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>DWORD (32 ビット)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>q</strong></p></td>
<td align="left"><p>QWORD (64 ビット)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>a</strong></p></td>
<td align="left"><p></p>
ASCII 文字列 (null で終わる文字列必須ではありません)</td>
</tr>
<tr class="even">
<td align="left"><p><strong>u</strong></p></td>
<td align="left"><p></p>
Unicode 文字列 (null で終わる文字列必須ではありません)</td>
</tr>
</tbody>
</table>

 

省略した場合*型*バイト値が使用されます。 ただし、使用する場合*フラグ*、省略できません*型*します。

<span id="_______sa______"></span><span id="_______SA______"></span> **sa**   
印刷可能な ASCII 文字列を含む任意のメモリを検索します。 使用して、 **l** *長さ*このような文字列の最小長を指定するフラグ。 既定の最小長には、3 文字です。

<span id="_______su______"></span><span id="_______SU______"></span> **su**   
印刷可能な Unicode 文字列を含む任意のメモリを検索します。 使用して、 **l** *長さ*このような文字列の最小長を指定するフラグ。 既定の最小長には、3 文字です。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
検索するメモリ領域を指定します。 この範囲は、使用する場合を除き、256 MB 以上にすることはできません、 **L?** 構文。 この構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
検索する 1 つまたは複数の値を指定します。 既定では、これらの値は、バイト値です。 メモリ内のさまざまな種類を指定する*型*します。 選択すると、その他のオプションによって、WORD、DWORD、または QWORD 値を指定する場合は、検索パターンを単一引用符で囲む必要があります (たとえば、 **'H'**)。 

```dbgcmd
0:000> s -d @rsp L1000000 'H'  
0000003f`ff07ec00  00000048 00000000 500c0163 00000000  H.......c..P....
0000003f`ff07ec50  00000048 00000000 00000080 00000000  H...............
0000003f`ff07efc0  00000048 00000000 400c0060 00000000  H.......`..@....
```

場合は、文字列を指定すると、ascii 型を使用して囲む二重引用符で (たとえば、 **"B7"**)。

```dbgcmd
0:000> s -a @rsp L10000000 "B7"  
0000003f`ff07ef0a  42 37 ff 7f 00 00 90 38-4e c2 6c 01 00 00 7d 26  B7.....8N.l...}&
0000003f`ff0ff322  42 37 ff 7f 00 00 f8 5d-42 37 ff 7f 00 00 20 41  B7.....]B7.... A
0000003f`ff0ff32a  42 37 ff 7f 00 00 20 41-42 37 ff 7f 00 00 98 59  B7.... AB7.....Y
```

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
指定したのと同じ型のオブジェクトの検索*オブジェクト*します。

<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
オブジェクトのアドレス、またはオブジェクトへのポインターのアドレスを指定します。 デバッガーを検索し、オブジェクトと同じ型のオブジェクトを*オブジェクト*を指定します。

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

メモリの操作とその他のメモリに関連するコマンドの説明の詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>コメント
-------

デバッガーには、指定したバイト パターンが検出されると、デバッガーを表示する最初のメモリ アドレス、*範囲*メモリ領域が、パターンが見つかった。 デバッガーで表示する、指定された一致する形式でその位置から開始されるメモリの抜粋*型*メモリの種類。 場合*型*は **、** または**u**メモリの内容と対応する ASCII または Unicode 文字が表示されます。

指定する必要があります、*パターン*(バイト単位) を一連のパラメーターをさまざまなを指定しない限り*型*値。 数値としてバイト値や ASCII 文字を入力できます。

-   数値の値は、現在の基数 (16、10、または 8) では数値として解釈されます。 既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。 既定の基数を指定して上書きできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。
    **注**  既定の基数は C++ の式を使用すると動作が異なります。 これらの式と基数の詳細については、次を参照してください。[を評価する式](evaluating-expressions.md)します。

     

-   ASCII 文字は、単一引用符で囲む必要があります。 C スタイルのエスケープ文字を使用することはできません (など '\\0' または'\\n')。

複数のバイトを指定する場合は、スペースで区切る必要があります。

**S、** と**s-u**それぞれ ASCII および Unicode 文字列の指定した場合のコマンドを検索します。 これらの文字列は、null で終了する必要はありません。

**S sa**と**s su**コマンドが指定されていない ASCII および Unicode 文字列を検索します。 これらは、すべての印刷可能な文字を含んでいるかどうかを確認するメモリの範囲をチェックする場合に便利です。 フラグ オプションを使用すると、検索する文字列の最小長を指定することができます。

例:次のコマンドは、ASCII 文字列の長さを検索します。 &gt;0000000140000000 で開始と終了時刻後で 400 バイト範囲内で 3 を = です。

```dbgcmd
s-sa 0000000140000000 L400
```

次のコマンドは、ASCII 文字列の長さを検索します&gt;0000000140000000 で開始と終了時刻後で 400 バイト範囲の 4 を =。

```dbgcmd
s -[l4]sa 0000000140000000 L400
```

次のコマンドは、同じが書き込み可能なメモリ領域に検索を制限します。

```dbgcmd
s -[wl4]sa 0000000140000000 L400
```

次のコマンドは、同じの動作が、一致のアドレスだけではなく、アドレス値が表示されます。

```dbgcmd
s -[1wl4]sa 0000000140000000 L400
```

**S v**コマンドと同じデータ型のオブジェクトの検索、*オブジェクト*オブジェクト。 このコマンドは、目的のオブジェクトが、C++ クラスまたは仮想関数テーブル (v テーブル) に関連付けられている別のオブジェクトである場合にのみ使用できます。 **S v**コマンドの検索、*範囲*このクラスの Vtable のアドレスのメモリ領域です。 複数 v テーブルは、このクラスに存在する場合、検索アルゴリズムは、すべての適切なバイト数で区切られた、これらのポインター値を探します。 デバッガーがオブジェクトとの出力のような--このオブジェクトの完全な情報のベース アドレスを返す任意の一致が見つかった場合、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

例:現在の基数は 16 を想定しています。 次の 3 つのコマンドの同じ操作を行うすべて: 0012FF5F を通じてメモリ場所 0012FF40「こんにちは」を検索します。

```dbgcmd
0:000> s 0012ff40 L20 'H' 'e' 'l' 'l' 'o' 
```

```dbgcmd
0:000> s 0012ff40 L20 48 65 6c 6c 6f 
```

```dbgcmd
0:000> s -a 0012ff40 L20 "Hello" 
```

これらのコマンドは、「こんにちは」の各の外観を検索し、各このようなパターンの--文字"H"のアドレスは、アドレスを返します。

デバッガーは、検索範囲内で完全に含まれているパターンのみを返します。 重複するパターンが正しく検出されます。 (つまり、パターン"QQQ"が見つかった 3 回"QQQQQ"にします。)

次の例では、使用する検索、*型*パラメーター。 このコマンドは、メモリの場所の 0012FF40 0012FF5F ダブル ワード 'VUTS' の使用を検索します。

```dbgcmd
0:000> s -d 0012ff40 L20 'VUTS' 
```

リトル エンディアンのコンピューターで 'VUTS' はバイト パターンのと同じ' 'T' 'U' 'V'。 ただし、単語、Dword、および QWORDs の検索には、正しくバイト境界である結果のみが返されます。

 

 





