---
title: tct (次の呼び出しまたはリターンまでトレース)
description: Tct コマンドでは、呼び出し命令に到達するまでプログラムを実行しますか、戻り命令。
ms.assetid: 059d8071-577f-4306-8273-8fdff6a80626
keywords:
- tct (トレースを次の呼び出しまたは戻り値に) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tct (Trace to Next Call or Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 43b24ebc7ea342f21c9570734235d3e81b7832b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380484"
---
# <a name="tct-trace-to-next-call-or-return"></a>tct (次の呼び出しまたはリターンまでトレース)


**Tct**命令を返したりするコマンドの呼び出し命令に到達するまでプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] tct [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
tct [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **tctr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 4 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
数を指定**呼び出す**または**返す**のデバッガーが発生する必要がありますのある手順、 **tct**終了するコマンド。 既定値は、1 つ。

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

**Tct**コマンドが実行を開始するようにターゲットを実行します。 デバッガーに達するまで、この実行を**呼び出す**または**返す**命令ブレークポイントに到達したか。

プログラム カウンターが既に入っている場合、**呼び出す**または**返す**命令、デバッガーは呼び出しや戻り値を追跡し、別に到達するまでの実行を続行**を呼び出す**または**返す**します。 呼び出しの実行ではなくこのトレースは、唯一の違いは、 **tct**と[ **pct (手順を次の呼び出しまたは戻り値)**](pct--step-to-next-call-or-return-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 このコマンドでは停止しません、**呼び出す**または**を返す**現在のソース行に関連付けられている命令。

 

 





