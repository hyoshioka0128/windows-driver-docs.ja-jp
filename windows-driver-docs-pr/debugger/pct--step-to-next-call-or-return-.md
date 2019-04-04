---
title: pct (手順を次の呼び出しまたは戻り値)
description: Pct コマンドは、呼び出し命令または戻り値の命令に到達するまでプログラムを実行します。
ms.assetid: ff4b5708-b9d0-4809-9fe4-9a22d4cacbc0
keywords:
- pct (手順を次の呼び出しまたは返された場合) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pct (Step to Next Call or Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84ff99ce4d7c55d80f6fe905fbb41a429335c453
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550463"
---
# <a name="pct-step-to-next-call-or-return"></a>pct (手順を次の呼び出しまたは戻り値)


**Pct**コマンド呼び出し命令または戻り値の命令に到達するまでプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] pct [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
pct [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 を通じて登録の表示を無効にすることができます、 **pctr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 それ以外の場合、デバッガーは、命令、命令ポインターが指すを開始します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
数を指定**呼び出す**または**返す**を停止するには、このコマンドの指示発生する必要があります。 既定値は、1 つ。

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

**Pct**コマンドが実行を開始するようにターゲットを実行します。 呼び出しまで、この実行または**返す**命令に到達するか、またはブレークポイントが検出されました。

プログラム カウンターが既に入っている場合、**呼び出す**または**返す**命令では、すべての呼び出しまたは戻り値が実行されます。 別まで実行が続行されますこの呼び出しまたは戻り値が返された後**呼び出す**または**返す**に到達します。 呼び出しのトレースではなくこの実行では、唯一の違いは、 **pct**と[ **tct (トレースを次の呼び出しまたは戻り値に)**](tct--trace-to-next-call-or-return-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 **Pct**コマンドでは停止しません、**呼び出す**または**返す**現在のソース行に関連付けられている命令。

 

 





