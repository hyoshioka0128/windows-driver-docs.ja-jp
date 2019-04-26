---
title: ph (次の分岐命令までステップ実行)
description: Ph コマンドは、分岐命令の任意の種類に達するまで、条件付きまたは無条件分岐、呼び出し、戻り値は、システムなどの呼び出しでプログラムを実行します。
ms.assetid: ba4699d3-9872-4deb-96c7-e8b54c1d8ec6
keywords:
- ph (分岐命令を次に手順) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ph (Step to Next Branching Instruction)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a50f23f58d2541d693bae791daa846acbab2a41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352913"
---
# <a name="ph-step-to-next-branching-instruction"></a>ph (次の分岐命令までステップ実行)


**Ph**コマンドは、分岐命令の任意の種類に達するまで、条件付きまたは無条件分岐、呼び出し、戻り値は、システムなどの呼び出しにプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] ph [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
ph [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **phr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 それ以外の場合、デバッガーは、命令、命令ポインターが指すを開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
停止するには、このコマンドの発生する必要がある分岐命令の数を指定します。 既定値は、1 つ。

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

関連するコマンドの詳細については、次を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

**Ph**コマンドが実行を開始するようにターゲットを実行します。 この実行では、分岐命令に達したか、ブレークポイントに到達するまで続行されます。

プログラム カウンターが既に分岐命令である場合は、全体の分岐命令が実行されます。 この分岐命令が返された後、別の分岐命令に到達するまで実行が続行されます。 呼び出しのトレースではなくこの実行では、唯一の違いは、 **ph**と[**番目 (トレースを次の分岐命令)**](th--trace-to-next-branching-instruction-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 **Ph**コマンドは、現在のソース行に関連付けられている分岐命令では停止しません。

 

 





