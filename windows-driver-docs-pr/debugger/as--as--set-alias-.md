---
title: as、aS (エイリアスの設定)
description: 同様に、コマンドは、新しいエイリアスを定義または、既存のものを再定義します。
ms.assetid: 6e42122b-5a18-403b-a19a-1346bea8da12
keywords:
- デバッグ (セットの別名) Windows と同様
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- as, aS (Set Alias)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fc6fe184b81ddf621165be258a5c529c13bd40fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354694"
---
# <a name="as-as-set-alias"></a>as、aS (エイリアスの設定)


**として**と**として**コマンドは、新しいエイリアスの定義や、既存のものを再定義します。

```dbgcmd
as Name EquivalentLine 
aS Name EquivalentPhrase 
aS Name "EquivalentPhrase" 
as /e Name EnvironmentVariable 
as /ma Name Address 
as /mu Name Address 
as /msa Name Address 
as /msu Name Address 
as /x Name Expression 
aS /f Name File 
as /c Name CommandString 
```

## <a name="span-idddkcmdsetaliasdbgspanspan-idddkcmdsetaliasdbgspanparameters"></a><span id="ddk_cmd_set_alias_dbg"></span><span id="DDK_CMD_SET_ALIAS_DBG"></span>パラメーター


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
エイリアス名を指定します。 この名前は、スペースまたは ENTER キー入力が含まれていないと、"as"、"al"で始まらない任意のテキスト文字列「と」または"ad"。 *名前*は大文字小文字を区別します。

<span id="_______EquivalentLine______"></span><span id="_______equivalentline______"></span><span id="_______EQUIVALENTLINE______"></span> *EquivalentLine*   
エイリアス相当するものを指定します。 *EquivalentLine*は大文字小文字を区別します。 間に少なくとも 1 つの領域を追加する必要があります*名前*と*EquivalentLine*します。 これら 2 つのパラメーター間の空白の数は重要ではありません。 ありません、エイリアスと同等には、先頭のスペースが含まれています。 これらのスペース後*EquivalentLine*行の残りの部分が含まれています。 セミコロン、引用符、およびスペースは、リテラル文字として扱われ、末尾のスペースが含まれています。

<span id="_______EquivalentPhrase______"></span><span id="_______equivalentphrase______"></span><span id="_______EQUIVALENTPHRASE______"></span> *EquivalentPhrase*   
エイリアス相当するものを指定します。 *EquivalentPhrase*は大文字小文字を区別します。 間に少なくとも 1 つの領域を追加する必要があります*名前*と*EquivalentPhrase*します。 これら 2 つのパラメーター間の空白の数は重要ではありません。 ありません、エイリアスと同等には、先頭のスペースが含まれています。

囲みます*EquivalentPhrase*引用符 (")。 引用符を使用するかどうかにかかわらず*EquivalentPhrase*スペース、コンマ、および単一引用符 (') に含めることができます。 囲んだ場合*EquivalentPhrase*引用符で含めることができますが、セミコロン、引用符を追加できません。 囲まなかった場合*EquivalentPhrase*引用符で最初の文字以外の任意の場所での引用符を含めるできますが、セミコロンを含めることはできません。 末尾のスペースは、引用符を使用するかどうかに関係なく含まれています。

<span id="________e______"></span><span id="________E______"></span> **/e**   
環境変数にエイリアスと等価の等値を設定*EnvironmentVariable*を指定します。

<span id="_______EnvironmentVariable______"></span><span id="_______environmentvariable______"></span><span id="_______ENVIRONMENTVARIABLE______"></span> *EnvironmentVariable*   
エイリアスと同等の決定に使用される環境変数を指定します。 デバッガーの環境を使用すると、ターゲットではなくの。 コマンド プロンプト ウィンドウで、デバッガーを開始した場合は、そのウィンドウで環境変数が使用されます。

<span id="________ma______"></span><span id="________MA______"></span> **/ma**   
Null で終わる ASCII 文字列で始まるエイリアスと等価の等値に設定*アドレス*します。

<span id="________mu______"></span><span id="________MU______"></span> **/mu**   
Null で終わる Unicode 文字列で始まるエイリアスと等価の等値に設定*アドレス*します。

<span id="________msa______"></span><span id="________MSA______"></span> **/msa**   
エイリアスと等価の等値を ANSI に設定\_文字列構造体にある*アドレス*します。

<span id="________msu______"></span><span id="________MSU______"></span> **/msu**   
エイリアスと等価の等値を UNICODE に設定\_文字列構造体にある*アドレス*します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
エイリアスと同等の決定に使用される仮想メモリの場所を指定します。

<span id="________x______"></span><span id="________X______"></span> **/x**   
エイリアスと等価の等値、64 ビットの値に設定*式*します。

<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *式*   
評価する式を指定します。 この値になります、エイリアスと同じです。 構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

<span id="________f______"></span><span id="________F______"></span> **/f**   
内容をエイリアスと等価の等値の設定、*ファイル*ファイル。 常に使用する必要があります、 **/f**スイッチと共に**として**ではなく**として**します。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *ファイル*   
ファイルの内容にエイリアスを指定と同じです。 *ファイル*、スペースを含めることができますが、決して囲みます*ファイル*引用符で囲んで指定します。 無効なファイルを指定する場合は、「メモリ不足」エラー メッセージが表示されます。

<span id="________c______"></span><span id="________C______"></span> **/c**   
コマンドの出力にエイリアスと等価の等値を設定*クラスヒント*を指定します。 エイリアスと同等には、コマンド表示内に含まれているし、(1 つのコマンドを指定する) 場合でも、各コマンドの表示の末尾に改行文字を返す場合、キャリッジ リターンが含まれます。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
出力に、エイリアス コマンドを指定と同じです。 この文字列は、セミコロンで区切られたコマンドの任意の数を含めることができます。

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

エイリアスを使用する方法の詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

<a name="remarks"></a>注釈
-------

すべてのスイッチを使用しない場合、**として**コマンドは、行の残りの部分を使用するエイリアスと同等にします。

終了することができます、**として**コマンドをセミコロンで区切ります。 この手法は、すべてのコマンドを 1 行に配置するときに、スクリプトで役に立ちます。 セミコロンの後の行の部分は、エイリアスの拡張を必要とする場合をする必要がありますで囲むことの行の 2 番目の部分はその新しいブロックに注意してください。 次の例では、0x6、予想される出力を生成します。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .block{.echo myAlias}
0x6
```

新しいブロックを省略した場合、予想される出力は取得できません。 新しく設定の拡張エイリアスが動作しないまで、新しいコード ブロックが入力されるためです。 次の例では、新しいブロックを省略すると、出力は、テキスト"myAlias"0x6 予期される値の代わりにします。

```dbgcmd
0:001> aS /x myAlias 5 + 1; .echo myAlias
myAlias
```

スクリプトでエイリアスの使用に関する詳細については、次を参照してください。 [Using エイリアス](using-aliases.md)します。

使用する場合、 **/e**、 **/ma**、 **/mu**、 **/msa**、 **/msu**、または **/x**切り替えるには、**として**と**として**コマンドでは、同じ機能し、セミコロンが発生した場合に、コマンドが終了します。

場合*名前*は既に別名が再定義されている既存のエイリアスの名前。

使用することができます、**として**または**として**コマンドを作成またはという名前のユーザーの任意のエイリアスを変更します。 固定名のエイリアス ($u0 に u9 $) を制御するコマンドを使用することはできません。

使用することができます、 **/ma**、 **/mu**、 **/msa**、 **/msu**、 **/f**、および **/c**改行コードを含むエイリアスを作成するスイッチを返します。 ただし、シーケンス内の複数のコマンドを実行するキャリッジ リターンを含むエイリアスを使用することはできません。 代わりに、セミコロンを使用する必要があります。

 

 





