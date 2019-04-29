---
title: .enable_long_status (長整数型の表示を有効にする)
description: .Enable_long_status コマンドでは、10 進形式または既定の基数でデバッガーが長整数を表示するかどうかを指定します。
ms.assetid: e08f5a40-5246-4120-ae43-37e876269463
keywords:
- 長整数の表示 (.enable_long_status) コマンドを有効にします。
- .enable_long_status (Long 整数表示を有効にする) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .enable_long_status (Enable Long Integer Display)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2faea3fce198d956ccf0d8652851b925c96b4dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336776"
---
# <a name="enablelongstatus-enable-long-integer-display"></a>リストア\_長い\_状態 (Long 整数の表示を有効にする)


**リストア\_長い\_状態**コマンドでは、10 進形式または既定の基数でデバッガーが長整数を表示するかどうかを指定します。

```dbgcmd
.enable_long_status 0 
.enable_long_status 1
```

## <a name="span-idddkmetaenablelongintegerdisplaydbgspanspan-idddkmetaenablelongintegerdisplaydbgspanparameters"></a><span id="ddk_meta_enable_long_integer_display_dbg"></span><span id="DDK_META_ENABLE_LONG_INTEGER_DISPLAY_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
10 進形式では、すべての長整数を表示します。 これは、デバッガーの既定の動作です。

<span id="_______1______"></span> **1**   
既定の基数では、すべての長整数を表示します。

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

**リストア\_長い\_状態**コマンドの出力に影響する、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

、WinDbg で**リストア\_長い\_状態**の表示にも影響、 [[ローカル] ウィンドウ](locals-window.md)と

[ウォッチ] ウィンドウ。 これらのウィンドウが自動的に更新を発行した後**リストア\_長い\_状態**します。

このコマンドでは、長整数の表示のみに影響します。 制御する標準の整数表示されるか 10 進形式または既定の基数で、使用、 [ **.force\_基数\_出力 (整数の基数を使用して)** ](-force-radix-output--use-radix-for-integers-.md)コマンド。

**注**   、 [ **dv (ローカル変数の表示)** ](dv--display-local-variables-.md)コマンドは、現在の基数での長整数を常に表示されます。

 

既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。

 

 





