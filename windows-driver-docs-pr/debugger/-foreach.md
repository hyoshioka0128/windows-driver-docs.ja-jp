---
title: .foreach
description: .Foreach トークンでは、1 つまたは複数のデバッガー コマンドの出力を解析し、この出力で各値を 1 つまたは複数の他のコマンドを入力として使用します。
ms.assetid: 646c86c2-a436-43d6-b0d8-32dbd423120e
keywords:
- デバッグ .foreach Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .foreach
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 630844f3d36619d9f8bb03bde1bb91e93cdf8b20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336619"
---
# <a name="foreach"></a>.foreach


**.Foreach**トークンは、1 つの出力を解析します。 または、デバッガーの詳細については、コマンドとはこの出力で各値を 1 つまたは複数のその他のコマンドを入力として使用します。

```dbgcmd
.foreach [Options] ( Variable  { InCommands } ) { OutCommands } 

.foreach [Options] /s ( Variable  "InString" ) { OutCommands } 

.foreach [Options] /f ( Variable  "InFile" ) { OutCommands } 
```

## <a name="span-idddktokenforeachdbgspanspan-idddktokenforeachdbgspansyntax-elements"></a><span id="ddk_token_foreach_dbg"></span><span id="DDK_TOKEN_FOREACH_DBG"></span>構文要素


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の組み合わせを指定できます。

<span id="_pS_InitialSkipNumber"></span><span id="_ps_initialskipnumber"></span><span id="_PS_INITIALSKIPNUMBER"></span>**/pS** *InitialSkipNumber*  
スキップする初期のトークンをによりします。 *InitialSkipNumber*は渡されません出力トークンの数を指定します。 指定した*OutCommands*します。

<span id="_ps_SkipNumber"></span><span id="_ps_skipnumber"></span><span id="_PS_SKIPNUMBER"></span>**/ps** *SkipNumber*  
繰り返しコマンドが処理されるたびにスキップするトークンをによりします。 たびに、トークンが渡されますを指定した*OutCommands*、トークンの値と等しい数*SkipNumber*は無視されます。

<span id="_______Variable______"></span><span id="_______variable______"></span><span id="_______VARIABLE______"></span> *変数*   
変数名を指定します。 この変数は内の各コマンドからの出力を保持するために使用されます、 *InCommands*文字列; を参照する*変数*に渡されるパラメーターの名前で、 *OutCommands*. 文字列の 16 進数の数字を渡すこともできますを使用して、任意の英数字の文字列を使用できますか、デバッガー コマンドはお勧めしません。 名前が使用されている場合*変数*、既存のグローバル変数、ローカル変数、またはエイリアスと一致するそれらの値は受けていません、 **.foreach**コマンド。

<span id="_______InCommands______"></span><span id="_______incommands______"></span><span id="_______INCOMMANDS______"></span> *InCommands*   
出力結果が解析されます。 1 つまたは複数のコマンドを指定します結果として得られるトークンに渡される*OutCommands*します。 出力*InCommands*は表示されません。

<span id="_______InString______"></span><span id="_______instring______"></span><span id="_______INSTRING______"></span> *InString*   
併用 **/s**します。 解析される文字列を指定します結果として得られるトークンに渡される*OutCommands*します。

<span id="_______InFile______"></span><span id="_______infile______"></span><span id="_______INFILE______"></span> *InFile*   
併用 **/f**します。 解析されるテキスト ファイルを指定します結果として得られるトークンに渡される*OutCommands*します。 ファイル名*InFile*引用符で囲む必要があります。

<span id="_______OutCommands______"></span><span id="_______outcommands______"></span><span id="_______OUTCOMMANDS______"></span> *OutCommands*   
トークンごとに実行される 1 つまたは複数のコマンドを指定します。 たびに、*変数*文字列が現在のトークンで置き換えられます。

**注**  ときに文字列*変数*内に表示する*OutCommands*には、スペースで囲む必要があります。 使用しない場合は、現在のトークンの値で置き換えられないする他のテキスト - かっこもに隣接する場合、 [ **$ {} (別名インタープリター)** ](-------alias-interpreter-.md)トークンです。

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のコントロール フロー トークンと、デバッガー コマンド プログラムでの使用については、次を参照してください。[を使用してデバッガー コマンド プログラム](using-debugger-command-programs.md)します。

<a name="remarks"></a>コメント
-------

ときに出力を*InCommands*、 *InString*文字列、または*InFile*ファイルの解析、任意の数のスペース、タブや改行を 1 つの区切り記号として扱われます。 置換に使用するテキストの結果として得られる要素の各*変数*内が表示されたら*OutCommands*します。

次の例に示します、 **.foreach**ステートメントを使用する、 [ **dds** ](dds--dps--dqs--display-words-and-symbols-.md)コマンド ファイルで見つかった各トークンを*myfile.txt*:

```dbgcmd
0:000> .foreach /f ( place "g:\myfile.txt") { dds place } 
```

**/PS**と **/ps**を指定した特定のトークンのみを渡すフラグを使用できる*OutCommands*します。 たとえば、次のステートメントが内の最初の 2 つのトークンをスキップ、 *myfile.txt*ファイルを開き、3 番目に渡す[ **dds**](dds--dps--dqs--display-words-and-symbols-.md)します。 渡される各トークンの後に 4 つのトークンはスキップされます。 その結果、 **dds**し、3 番目、8、13、18th、および 23 のトークンで使用します。

```dbgcmd
0:000> .foreach /pS 2 /ps 4 /f ( place "g:\myfile.txt") { dds place } 
```

使用する例について、 **.foreach**トークンを参照してください[デバッガー コマンド プログラム例](debugger-command-program-examples.md)します。

 

 





