---
title: p (ステップ)
description: P コマンドでは、1 つの命令またはソース行を実行し、必要に応じてレジスタとフラグのすべての結果の値を表示します。
ms.assetid: 4ee24e76-b751-4346-80af-d481d9513ce0
keywords:
- p (手順) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- p (Step)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cac8b8f3578104ecf07d0ed4150b77b6e2d22e00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532689"
---
# <a name="p-step"></a>p (ステップ)


**P**コマンドは、1 つの命令またはソース行を実行し、必要に応じてレジスタとフラグのすべての結果の値を表示します。 ときにサブルーチンの呼び出しまたは割り込みが発生する、1 つのステップとして扱われます。

ユーザー モード

```dbgcmd
[~Thread] p[r] [= StartAddress] [Count] ["Command"] 
```

カーネル モード

```dbgcmd
p[r] [= StartAddress] [Count] ["Command"] 
```

## <a name="span-idddkcmdstepdbgspanspan-idddkcmdstepdbgspanparameters"></a><span id="ddk_cmd_step_dbg"></span><span id="DDK_CMD_STEP_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **pr**、 [ **tr**](t--trace-.md)、または .prompt\_-reg コマンドを許可します。 これらのコマンドの 3 つすべてが同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
実行を開始するアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
停止する前にステップ実行するには、手順またはソース行の数を指定します。 別のアクションとして各ステップが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 既定値は、1 つ。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
ステップの実行後に実行するデバッガー コマンドを指定します。 このコマンドは、標準の前に実行**p**結果が表示されます。 使用する場合は*カウント*、すべてのステップ実行が完了した後 (ただし、最後の手順の結果が表示される前に) 指定されたコマンドを実行します。

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

発行の詳細については、 **p**コマンドとの概要については、関連するコマンドを参照してください[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

指定すると*カウント*、ステップ実行には、それぞれの命令が表示されます。

デバッガーが発生した場合、**呼び出す**ブレークポイントに到達しない限り、命令またはステップ実行中に割り込み、というサブルーチンが完全に実行します。 コントロールには、呼び出しまたは割り込みの後に次の命令でデバッガーが返されます。

各ステップでは、1 つのアセンブリ命令またはモードのアセンブリまたはソース モードでデバッガーがかどうかに応じて、1 つのソース行を実行します。 使用して、 [ **l + t** ](l---l---set-source-options-.md) l t コマンドまたは WinDbg ツールバーのボタンと、これらのモードを切り替えます。

何度もをステップ実行、WinDbg ではすぐに、各手順の後にデバッグ情報ウィンドウが更新されます。 この更新プログラムには、低速の応答時間が発生する場合は、使用[**明解\_ui (WinDbg インターフェイスの中断)** ](-suspend-ui--suspend-windbg-interface-.md)をこれらのウィンドウの更新を一時停止します。

 

 





