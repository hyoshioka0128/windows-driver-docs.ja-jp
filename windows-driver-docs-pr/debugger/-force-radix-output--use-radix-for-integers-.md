---
title: .force_radix_output (整数に基数を使用)
description: .Force_radix_output コマンドでは、10 進形式または既定の基数で整数を表示するかどうかを指定します。
ms.assetid: 9ce79919-69fd-426f-8de1-34d0721c35a5
keywords:
- 整数 (.force_radix_output) コマンドの基数を使用します。
- .force_radix_output (整数の基数を使用して) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .force_radix_output (Use Radix for Integers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5ca7d5faacd29e0cf8d5c473b56811e02e23a946
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336637"
---
# <a name="forceradixoutput-use-radix-for-integers"></a>.force\_基数\_出力 (整数の基数を使用)


**.Force\_基数\_出力**コマンドでは、10 進形式または既定の基数で整数を表示するかどうかを指定します。

```dbgcmd
.force_radix_output 0 
.force_radix_output 1 
```

## <a name="span-idddkmetauseradixforintegersdbgspanspan-idddkmetauseradixforintegersdbgspanparameters"></a><span id="ddk_meta_use_radix_for_integers_dbg"></span><span id="DDK_META_USE_RADIX_FOR_INTEGERS_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
10 進形式の (長整数) を除くすべての整数を表示します。 これは、デバッガーの既定の動作です。

<span id="_______1______"></span> **1**   
既定の基数での (長整数) を除くすべての整数を表示します。

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
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**.Force\_基数\_出力**コマンドの出力に影響する、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

、WinDbg で **.force\_基数\_出力**の表示にも影響、 [[ローカル] ウィンドウ](locals-window.md)とウォッチ ウィンドウ。 選択またはクリアできます**常に表示番号の既定の基数**ローカルまたはウォッチのショートカット メニューの ウィンドウと同じ効果 **.force\_基数\_出力**します。 このコマンドを発行した後、これらのウィンドウが自動的に更新します。

**.Force\_基数\_出力**コマンドの標準の整数の表示のみに影響します。 10 進形式または既定の基数の長整数を表示するかどうかを指定するには、使用、 [**リストア\_長い\_状態 (Long 整数の表示を有効にする)** ](-enable-long-status--enable-long-integer-display-.md)コマンド。

既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

 

 





