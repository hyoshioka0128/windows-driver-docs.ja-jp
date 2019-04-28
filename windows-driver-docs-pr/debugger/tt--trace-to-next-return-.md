---
title: tt (次のリターンまでトレース)
description: Tt コマンドは、戻り命令に到達するまでプログラムを実行します。
ms.assetid: fbc6627f-62e0-4832-8da5-dd4d3323965a
keywords:
- tt (トレース [次へ] を返す) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tt (Trace to Next Return)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4116512a91c1bc7cb6e7fe36c1b522618d30c2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380784"
---
# <a name="tt-trace-to-next-return"></a>tt (次のリターンまでトレース)


**Tt**戻り命令に到達するまで、コマンドがプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] tt [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
tt [r] [= StartAddress] [Count] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **ttr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 4 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
数を指定**返す**のデバッガーが発生する必要がありますのある手順、 **th**終了するコマンド。 既定値は、1 つ。

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

**Tt**コマンドが実行を開始するようにターゲットを実行します。 この実行は、デバッガーに到達するまでは引き続き、**返す**命令ブレークポイントに到達したか

プログラム カウンターが既に入っている場合、**返す**命令、デバッガーは、戻り値を追跡し、別の実行を続行**返す**に到達します。 呼び出しの実行ではなくこのトレースは、唯一の違いは、 **tt**と[ **pt (手順 [次へ] を返す)**](pt--step-to-next-return-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 このコマンドでは停止しません、**返す**現在のソース行に関連付けられている命令。

 

 





