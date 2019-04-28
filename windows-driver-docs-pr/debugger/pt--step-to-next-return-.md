---
title: pt (次のリターンまでステップ実行)
description: Pt コマンドは、戻り命令に到達するまでプログラムを実行します。
ms.assetid: f4388953-4cb2-4df5-af8b-150e50ce765b
keywords:
- pt (手順を次の戻り値) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pt (Step to Next Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0dd03c8e5e5ffd01875c2b31a439d9acc4b0c929
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362392"
---
# <a name="pt-step-to-next-return"></a>pt (次のリターンまでステップ実行)


**Pt**戻り命令に到達するまで、コマンドがプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] pt [r] [= StartAddress] [Count] ["Command"]
```

カーネル モード

```dbgcmd
pt [r] [= StartAddress] [Count] ["Command"]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **ptr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 それ以外の場合、デバッガーは、命令、命令ポインターが指すを開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
数を指定**返す**を停止するには、このコマンドの指示発生する必要があります。 既定値は、1 つ。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
ステップの実行後に実行するデバッガー コマンドを指定します。 このコマンドは、標準の前に実行**pt**結果が表示されます。 使用する場合は*カウント*、すべてのステップ実行が完了した後 (ただし、最後の手順の結果が表示される前に) 指定されたコマンドを実行します。

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

**Pt**コマンドが実行を開始するようにターゲットを実行します。 までは引き続きこの実行を**返す**命令に到達するか、またはブレークポイントが検出されました。

プログラム カウンターが既に入っている場合、**返す**命令、全体の戻り値を実行します。 別まで実行が続行されますこの戻り値が返された後**返す**に到達します。 呼び出しのトレースではなくこの実行では、唯一の違いは、 **pt**と[ **tt ([次へ] を返すトレース)**](tt--trace-to-next-return-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 **Pt**コマンドでは停止しません、**返す**現在のソース行に関連付けられている命令。

次の例を使用して、 **pt**コマンドと共に、 **kb**スタック トレースを表示するコマンド。

```dbgcmd
0:000> pt "kb"
```

 

 





