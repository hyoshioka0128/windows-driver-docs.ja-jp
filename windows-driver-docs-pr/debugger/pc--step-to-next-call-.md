---
title: pc (次の呼び出しにステップ)
description: Pc のコマンドは、呼び出し命令に到達するまでプログラムを実行します。
ms.assetid: 4b9b786c-2ecc-44a6-a82b-0641d7991abc
keywords:
- デバッグ pc (次の呼び出しにステップ) Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pc (Step to Next Call)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afc399926d026638f79881c3fe5db27ef1ac5e3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560797"
---
# <a name="pc-step-to-next-call"></a>pc (次の呼び出しにステップ)


**Pc**コマンド呼び出し命令に到達するまでプログラムを実行します。

ユーザー モード

```dbgcmd
[~Thread] pc [r] [= StartAddress] [Count] 
```

カーネル モード

```dbgcmd
pc [r] [= StartAddress] [Count] 
```

## <a name="span-idddkcmdsteptonextcalldbgspanspan-idddkcmdsteptonextcalldbgspanparameters"></a><span id="ddk_cmd_step_to_next_call_dbg"></span><span id="DDK_CMD_STEP_TO_NEXT_CALL_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
実行を継続するスレッドを指定します。 その他のすべてのスレッドが固定されています。 構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 **pcr**、 [ **pr**](p--step-.md)、 [ **tr**](t--trace-.md)、または .prompt\_- reg コマンドを許可します。 これらすべてのコマンドの同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 それ以外の場合、デバッガーは、命令、命令ポインターが指すを開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
数を指定**呼び出す**を停止するには、このコマンドの指示、デバッガーに発生する必要があります。 既定値は、1 つ。

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

<a name="remarks"></a>注釈
-------

**Pc**コマンドが実行を開始するようにターゲットを実行します。 までは引き続きこの実行を**呼び出す**命令に到達するか、またはブレークポイントが検出されました。

プログラム カウンターが既に入っている場合、**呼び出す**命令、すべての呼び出しを実行します。 別まで実行が続行されますこの呼び出しが返された後**呼び出す**に到達します。 呼び出しのトレースではなくこの実行では、唯一の違いは、 **pc**と[ **tc (次の呼び出しをトレース)**](tc--trace-to-next-call-.md)します。

元のモードでは、複数のアセンブリ命令を 1 つのソース行を関連付けることができます。 **Pc**コマンドでは停止しません、**呼び出す**現在のソース行に関連付けられている命令。

 

 





