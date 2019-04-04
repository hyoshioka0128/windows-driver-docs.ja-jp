---
title: l+、l- (ソース オプションの設定)
description: L + l コマンド ライン オプションをソースの表示を制御し、ステップ実行オプションをプログラムのソースの設定とします。
ms.assetid: 7b169af0-e799-47eb-b197-c4408a755702
keywords:
- l +、l - (ソース オプションの設定) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- l+, l- (Set Source Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2afa93e9891c9e07c03c7af905a7f72064a19ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580410"
---
# <a name="l-l--set-source-options"></a>l+、l- (ソース オプションの設定)


<strong>L +</strong>と**l-** コマンド ライン オプションをソースの表示を制御し、ステップ実行オプションをプログラムのソースの設定。

```dbgcmd
l+Option 
l-Option 
l{+|-} 
```

## <a name="span-idddkcmdsetsourceoptionsdbgspanspan-idddkcmdsetsourceoptionsdbgspanparameters"></a><span id="ddk_cmd_set_source_options_dbg"></span><span id="DDK_CMD_SET_SOURCE_OPTIONS_DBG"></span>パラメーター


<span id="_________or_-"></span><span id="_________OR_-"></span> **+** または **-**  
指定したオプションが有効にするかどうかを指定します (プラス記号\[ + \]) またはオフになっています (マイナス記号\[ - \])。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span> *オプション*   
次のオプションの 1 つ。 オプションは、小文字である必要があります。

<span id="l"></span><span id="L"></span>**L**  
コマンド プロンプトで、ソース行番号を表示します。 L %.*ls または .prompt でソース行の表示を無効にできます\_-src を許可します。ソース行番号が表示され、ソース行が有効にする必要がありますは両方のメカニズムを表示します。

<span id="o"></span><span id="O"></span>**O**  
(ソース行と行番号) を除くすべてのメッセージを非表示にコードをステップ実行はときにします。 (、 **S**オプションをアクティブにする必要がありますも、 **o**まったく影響するオプションです)。

<span id="s"></span><span id="S"></span>**s**  
コマンド プロンプトで、ソース行とソース行番号を表示します。

<span id="t"></span><span id="T"></span>**t**  
開始[ソース モード](debugging-in-source-mode.md)します。 このモードが設定されていない場合に、デバッガーが[モードのアセンブリ](debugging-in-assembly-mode.md)します。

<span id="_"></span>**\\***  
オンまたはすべてのオプションをオフにします。

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

ソースのデバッグと関連するコマンドの詳細については、[元のモードでデバッグ](debugging-in-source-mode.md)を参照してください。 アセンブリの詳細については、デバッグ、および関連するコマンドを参照してください[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

<a name="remarks"></a>コメント
-------

省略した場合*オプション*、以前の set オプションが表示されます。 ここで、 **l +** と**l-** コマンドと同じ効果があります。 しかし、プラス記号を含める必要があります (**+**) またはマイナス記号 (-) の**l**コマンドを実行します。

1 つだけ含めることができます*オプション*たびにこのコマンドを発行します。 1 つ以上のオプションの一覧を表示する場合は、最初のオプションのみが検出されました。 ただし、このコマンドを繰り返し実行してオンまたはオフに多くのオプションを有効にできます。 (つまり、 **l + lst**がうまくいかないが**l + l; l + s; l + t**は希望する効果を実現します)。

指定した場合、 **s**とき、指定したかどうかに関係なく、コードをステップ実行オプション、ソース行および行番号が表示される、 **l**オプション。 **O**オプションには効果がないを指定しない限り、 **s**オプション。

行の番号を使用して読み込みを有効にしない限りソース行のオプションは有効になりません、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンドまたは[-行のコマンド ライン オプション](command-line-options.md). 既定では、これらのコマンドを使用していない場合に WinDbg がソース行のサポートをオンになり、CDB がオフにします。

 

 





