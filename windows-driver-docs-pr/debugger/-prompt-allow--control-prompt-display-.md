---
title: .prompt_allow (プロンプト表示の制御)
description: .Prompt_allow コマンドは、ステップ実行し、トレース中に、ターゲットの実行が停止されるたびに表示される情報を制御します。
ms.assetid: 916114f9-0a68-4423-ba28-a5f0da8a1af9
keywords:
- .prompt_allow (プロンプトを表示するコントロール) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .prompt_allow (Control Prompt Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec4492e245bdefabab5643f182e06b72cc0371a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334337"
---
# <a name="promptallow-control-prompt-display"></a>.prompt\_(プロンプトを表示するコントロール) を許可します。


**.Prompt\_許可**コマンド コントロールのステップ実行し、トレース中に、ターゲットの実行が停止されるたびに、どのような情報が表示されます。

```dbgcmd
.prompt_allow {+|-}Item [...] 
.prompt_allow 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="______________"></span> **+**    
ステップ実行、トレース、および実行のプロンプトには、指定した項目を表示します。 プラス記号 (+) の前にスペースを追加する必要がありますが、その後にスペースを追加することはできません。

<span id="_______-______"></span> **-**    
指定した項目がステップ実行、トレース、および実行のプロンプトに表示されないようにします。 マイナス記号 (-) の前にスペースを追加する必要がありますが、その後にスペースを追加することはできません。

<span id="_______Item______"></span><span id="_______item______"></span><span id="_______ITEM______"></span> *項目*   
項目を表示または非表示を指定します。 項目の数を指定することができます。 スペースで複数の項目を区切ります。 プラス記号 (+) または各項目の前にマイナス記号 (-) を追加する必要があります。 次のものを使用することができます。

<span id="dis"></span><span id="DIS"></span>**表示します。**  
現在の場所に逆アセンブルされた手順です。

<span id="ea"></span><span id="EA"></span>**ea**  
現在の命令の有効なアドレスです。

<span id="reg"></span><span id="REG"></span>**reg**  
最も重要なレジスタの現在の状態。 使用して登録の表示を無効にすることができます、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_-reg コマンドを許可します。 これらのコマンドの 3 つすべてが同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、次の「解説」セクションで説明した他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="src"></span><span id="SRC"></span>**src**  
現在の命令に対応するソース行。 L %.ls または .prompt を使用してソース行の表示を無効にできます\_-src; を許可するコマンド。 表示される両方のメカニズムをソース行の表示を有効にする必要があります。

<span id="sym"></span><span id="SYM"></span>**sym**  
現在の命令の記号。 このシンボルには、現在のモジュール、関数名、およびオフセットが含まれています。

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

実行に影響するコマンドの詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

使用することができます、 **.prompt\_許可**コマンド パラメーターを表示する項目が表示され、表示されません。 実行するたびに **.prompt\_許可**デバッガーは、指定した項目だけの状態を変更します。

既定では、すべての項目が表示されます。

L + os オプションは、このオプションを使用した場合のいずれかのオーバーライド、 **.prompt\_許可**以外のオプション**src**します。

次の例などの複雑なコマンドを使用することもできます。

```dbgcmd
0:000> .prompt_allow -reg -dis +ea 
Allow the following information to be displayed at the prompt:
(Other settings can affect whether the information is actually displayed)
   sym - Symbol for current instruction
    ea - Effective address for current instruction
   src - Source info for current instruction
Do not allow the following information to be displayed at the prompt:
   dis - Disassembly of current instruction
   reg - Register state
```

 

 





