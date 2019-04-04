---
title: pa (アドレスに手順)
description: Pa コマンドは、各ステップを表示する、指定されたアドレスが到達するまでプログラムを実行します。
ms.assetid: 497261a9-69fb-4df2-b342-cd62bda8a51f
keywords:
- pa (手順アドレスに) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pa (Step to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b00bb0951cb306f538499ea35fa52504121321d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537462"
---
# <a name="pa-step-to-address"></a>pa (アドレスに手順)


**Pa**コマンドは、各ステップを表示する、指定されたアドレスが到達するまでにプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] pa [r] [= StartAddress] StopAddress ["Command"]
```

カーネル モード

```dbgcmd
pa [r] [= StartAddress] StopAddress ["Command"]
```

## <a name="span-idddkcmdsteptoaddressdbgspanspan-idddkcmdsteptoaddressdbgspanparameters"></a><span id="ddk_cmd_step_to_address_dbg"></span><span id="DDK_CMD_STEP_TO_ADDRESS_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **par**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 それ以外の場合、デバッガーは、命令、命令ポインターが指すを開始します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span> *StopAddress*   
実行が停止するアドレスを指定します。 このアドレスは、命令の正確なアドレスと一致する必要があります。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
ステップの実行後に実行するデバッガー コマンドを指定します。 このコマンドは、標準の前に実行**pa**結果が表示されます。 使用する場合は*StopAddress*、後に、指定したコマンドが実行*StopAddress*に達した (ただし、最後の手順の結果が表示される前に)。

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

関連するコマンドの詳細については、[ターゲットを制御する](controlling-the-target.md)を参照してください。

<a name="remarks"></a>注釈
-------

**Pa**コマンドが実行を開始するようにターゲットを実行します。 この実行では、指定された命令に達したか、ブレークポイントに到達するまで続行されます。

**注**  命令がすべての仮想アドレス領域で指定された仮想アドレスに発生したときにカーネル モードでこのコマンドを使用する場合の実行を停止します。

 

この実行中には、すべての手順が明示的に表示されます。 呼び出された関数は、1 つの単位として扱われます。 そのため、このコマンドの表示は「を実行する場合のような[ **p (ステップ)** ](p--step-.md)プログラム カウンターが指定されたアドレスに到達するまで繰り返し。

たとえば、次のコマンドに明示的に手順をターゲット コード、現在の関数の戻り値のアドレスに到達するまでします。

```dbgcmd
0:000> pa @$ra 
```

次の例を使用して、 **pa**コマンドと共に、 **kb**スタック トレースを表示するコマンド。

```dbgcmd
0:000> pa 70b5d2f1 "kb"
```

 

 





