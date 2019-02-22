---
title: .kframes (スタックの長さの設定)
description: .Kframes コマンドでは、スタック トレースの表示の既定の長さを設定します。
ms.assetid: 4f11a197-add1-4957-8345-dfbdb2037605
keywords:
- スタックの長さ (.kframes) コマンドを設定します。
- .kframes (スタックの長さの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kframes (Set Stack Length)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6775751def8fa5a72ec6b191b660a11f22907ce7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529662"
---
# <a name="kframes-set-stack-length"></a>.kframes (スタックの長さの設定)


**.Kframes**コマンドは、スタック トレースの表示の既定の長さを設定します。

```dbgcmd
.kframes FrameCountDefault 
```

## <a name="span-idddkmetasetstacklengthdbgspanspan-idddkmetasetstacklengthdbgspanparameters"></a><span id="ddk_meta_set_stack_length_dbg"></span><span id="DDK_META_SET_STACK_LENGTH_DBG"></span>パラメーター


<span id="_______FrameCountDefault______"></span><span id="_______framecountdefault______"></span><span id="_______FRAMECOUNTDEFAULT______"></span> *FrameCountDefault*   
スタック トレース コマンドを使用する場合に表示するスタック フレームの数を指定します。

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

使用することができます、 **.kframes**スタック トレースの表示の既定の長さを設定するコマンド。 この長さは、フレームの数を制御する、 [ **k、kb、kp、kP、および kv** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを表示し、DWORD 数\_PTRs を**kd**コマンドが表示されます。

この既定の長さを使用してオーバーライドすることができます、 *FrameCount*または*WordCount*これらのコマンドのパラメーター。

決して発行した場合、 **.kframes**コマンドで、既定の数は 20 ですが (0x14)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

 

 






