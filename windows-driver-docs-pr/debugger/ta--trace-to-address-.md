---
title: ta (アドレスまでトレース)
description: Ta コマンドの実行プログラムまで、指定したアドレスに達すると、各ステップ (呼び出された関数内のステップを含む) を表示します。
ms.assetid: 99741659-dd43-44ea-ac27-06d821b47fbe
keywords:
- ta (トレース アドレスに) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ta (Trace to Address)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fda2fbf6e537c8b88a0fb9349da4a942791ec88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581405"
---
# <a name="ta-trace-to-address"></a>ta (アドレスまでトレース)


**Ta**コマンドは、各ステップ (呼び出された関数内のステップを含む) を表示する、指定されたアドレスが到達するまでにプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] ta [r] [= StartAddress] StopAddress 
```

カーネル モード

```dbgcmd
ta [r] [= StartAddress] StopAddress 
```

## <a name="span-idddkcmdtracetoaddressdbgspanspan-idddkcmdtracetoaddressdbgspanparameters"></a><span id="ddk_cmd_trace_to_address_dbg"></span><span id="DDK_CMD_TRACE_TO_ADDRESS_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **tar**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、使用してこれらのいずれかのオーバーライドをすべて以前を使用してこれらのコマンド。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 4 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______StopAddress______"></span><span id="_______stopaddress______"></span><span id="_______STOPADDRESS______"></span> *StopAddress*   
実行を停止するためのアドレスを指定します。 このアドレスは、命令の正確なアドレスと一致する必要があります。

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

<a name="remarks"></a>コメント
-------

**Ta**コマンドが実行を開始するようにターゲットを実行します。 この実行では、指定された命令に達したか、ブレークポイントに到達するまで続行されます。

**注**  を使用する場合、 **ta**コマンドをカーネル モードでは、すべての仮想アドレス領域で指定された仮想アドレスに命令が検出されたときに実行が停止します。

 

この実行中には、すべての手順が明示的に表示されます。 関数が呼び出された場合、デバッガーは、その関数を使用もトレースします。 そのため、このコマンドの表示のようを実行した場合に表示[ **t (トレース)** ](t--trace-.md)プログラム カウンターが指定されたアドレスに到達するまで繰り返し。

たとえば、次のコマンド明示的にトレース ターゲット コードを現在の関数の戻り値のアドレスに到達するまでします。

```dbgcmd
0:000> ta @$ra 
```

 

 





