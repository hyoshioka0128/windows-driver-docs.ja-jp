---
title: th (次の分岐命令までトレース)
description: 番目のコマンドは、任意の種類の条件付きなどの分岐命令に到達または無条件分岐、呼び出しから制御が戻るし、システムの呼び出しまで、プログラムを実行します。
ms.assetid: 42b7ceb6-c507-45b3-9186-0a4014b68a28
keywords:
- th (トレースを次の分岐命令に) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- th (Trace to Next Branching Instruction)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e3eb9dcfc2b3018c2735518250b814e02d5f7e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570994"
---
# <a name="th-trace-to-next-branching-instruction"></a>th (次の分岐命令までトレース)


**Th**コマンドなど、条件付き分岐命令の任意の種類に達するまでまたは無条件分岐、呼び出しから制御が戻るシステム呼び出しでプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] th [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
th [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、**その**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 4 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
デバッガーが発生する必要があります分岐命令の数を指定します、 **th**終了するコマンド。 既定値は、1 つ。

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

**Th**コマンドが実行を開始するようにターゲットを実行します。 実行は、デバッガーは、分岐命令に達したか、ブレークポイントに到達したまで続行されます。

プログラム カウンターが既に分岐命令である場合は、デバッガーは分岐命令を追跡し、もう 1 つの分岐命令に到達するまでの実行を続けます。 呼び出しの実行ではなくこのトレースは、唯一の違いは、 **th**と[ **ph (分岐命令を次に手順)**](ph--step-to-next-branching-instruction-.md)します。

**th**はすべてのライブ セッションを使用できます。 この可用性の主な違いは、 **th**と[ **tb (トレースを次の分岐)**](tb--trace-to-next-branch-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 このコマンドは、現在のソース行に関連付けられている分岐命令では停止しません。

 

 





