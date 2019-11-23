---
title: l+、l- (ソース オプションの設定)
description: L + と l コマンドは、ソースの表示とプログラムのステップ実行オプションを制御するソース行オプションを設定します。
ms.assetid: 7b169af0-e799-47eb-b197-c4408a755702
keywords:
- l +、l-(ソースオプションの設定) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- l+, l- (Set Source Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 040fa89e792f597d10da46d4668f6460079dc21b
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038095"
---
# <a name="l-l--set-source-options"></a>l+、l- (ソース オプションの設定)

<strong>L +</strong>と**l**コマンドは、ソースの表示とプログラムのステップ実行オプションを制御するソース行オプションを設定します。

```dbgcmd
l+Option
l-Option
l{+|-}
```

## <a name="span-idddk_cmd_set_source_options_dbgspanspan-idddk_cmd_set_source_options_dbgspanparameters"></a><span id="ddk_cmd_set_source_options_dbg"></span><span id="DDK_CMD_SET_SOURCE_OPTIONS_DBG"></span>パラメータ

<span id="_________or_-"></span><span id="_________OR_-"></span> **+** または **-**  
特定のオプションを有効にするかどうかを指定します (正符号 \[+\]) またはオフ (マイナス記号 \[-\])。

<span id="_______Option______"></span><span id="_______option______"></span><span id="_______OPTION______"></span>*オプション*次のいずれかのオプション。 オプションは小文字で指定する必要があります。

<span id="l"></span><span id="L"></span>**左右**  
コマンドプロンプトでソース行番号を表示します。 L ls または .prompt でソース行の表示を無効にできます\_-src を許可します。 ソース行番号が表示されるようにするには、両方のメカニズムを使用してソース行の表示を有効にする必要があります。

<span id="o"></span><span id="O"></span>**i/o**  
コードをステップ実行するときに、すべてのメッセージ (ソース行と行番号以外) を非表示にします。 **O**オプションを有効にするには、 **s**オプションもアクティブになっている必要があります。

<span id="s"></span><span id="S"></span>**2$s**  
コマンドプロンプトにソース行とソース行番号を表示します。

<span id="t"></span><span id="T"></span> **\t**  
[ソースモード](debugging-in-source-mode.md)を開始します。 このモードが設定されていない場合、デバッガーは[アセンブリモード](debugging-in-assembly-mode.md)になります。

<span id="_"></span>**\***  
すべてのオプションをオンまたはオフにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Modes</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Platforms</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 ### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ソースデバッグと関連コマンドの詳細については、「[ソースモードでのデバッグ](debugging-in-source-mode.md)」を参照してください。 アセンブリデバッグと関連コマンドの詳細については、「[アセンブリモードでのデバッグ](debugging-in-assembly-mode.md)」を参照してください。

<a name="remarks"></a>注釈
-------

*オプション*を省略した場合は、以前に設定したオプションが表示されます。 この場合、 **l +** と**l**コマンドは同じ効果を持ちます。 ただし、 **l**コマンドを機能させるには、プラス記号 ( **+** ) またはマイナス記号 (-) を含める必要があります。

このコマンドを実行するたびに、*オプション*を1つだけ含めることができます。 複数のオプションを指定した場合は、最初のオプションのみが検出されます。 ただし、このコマンドを繰り返し実行することで、必要な数のオプションを有効または無効にすることができます。 (つまり、l + **lst**は機能しませんが、l + **l、l + s、l + t**は必要な効果を実現します)。

**S**オプションを指定すると、コードをステップ実行するときに、 **l**オプションを指定したかどうかに関係なく、ソース行と行番号が表示されます。 **S**オプションを指定しない限り、 **o**オプションは無効です。

[線] [ **([ソース行のサポートの切り替え])** ](-lines--toggle-source-line-support-.md)コマンドまたは [ [-lines] コマンドラインオプション](command-line-options.md)を使用して行番号の読み込みを有効にしない限り、ソース行のオプションは有効になりません。 既定では、これらのコマンドを使用していない場合、WinDbg はソースラインのサポートを有効にし、CDB はオフにします。
