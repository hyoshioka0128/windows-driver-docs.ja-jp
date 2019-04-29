---
title: ndiskd.ndisref
description: Ndiskd.ndisref 拡張機能は、追跡対象の参照カウントのデバッグ ログを表示します。
ms.assetid: 6860A567-1017-4184-B8DF-157467360FB9
keywords:
- デバッグ ndiskd.ndisref Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisref
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 23e55a3d327c338fb24340518a700c7697aa1376
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336068"
---
# <a name="ndiskdndisref"></a>!ndiskd.ndisref


**! Ndiskd.ndisref**拡張機能は、追跡対象の参照カウントのデバッグ ログを表示します。

```console
!ndiskd.ndisref [-handle <x>] [-tagtype <str>] [-stacks] [-tag <str>] [-refdebug] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 Refcount ブロックのハンドル。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span> *-tagtype*   
タグの列挙型。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-履歴*   
(該当する場合) は、スタック トレースに含まれています。

<span id="_______-tag______"></span><span id="_______-TAG______"></span> *-tag*   
制限は、1 つのタグを表示します。

<span id="_______-refdebug______"></span><span id="_______-REFDEBUG______"></span> *-refdebug*   
使用可能な場合、詳細なデバッグ ログを示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

次の例では、通過する NDIS ミニポート ドライバーのハンドル、 **! ndiskd.ndisref**拡張機能のドライバーの参照カウントのブロックを表示します。 最初に、実行[ **! ndiskd.minidriver** ](-ndiskd-minidriver.md)でパラメーターのないシステム上のすべてのミニポート ドライバーの一覧を参照してください。 次の例の出力で ffffdf801418d650 kdnic ドライバーのハンドルを探します。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

ミニポート ドライバーのハンドルを使用して入力し、 **! ndiskd.ndisref-処理**ミニポート ドライバーの参照カウントのブロックを表示するコマンド。 次の例では、簡潔にするための excised refcount ブロックの中央が。

```console
3: kd> !ndiskd.ndisref ffffdf801418d650


REFCOUNT BLOCK

    Tag                                    Number of references                 
    0n0                                    0n6293             Show stacks
    0n1                                    0n1045             Show stacks
    0n2                                    0n4294966717       Show stacks
    0n5                                    0n25048            Show stacks
    0n18                                   0n4294967293       Show stacks
    0n19                                   0n4294967295       Show stacks
    0n21                                   0n4294967036       Show stacks
    0n23                                   0n30818            Show stacks
    0n24                                   0n24693            Show stacks
    0n25                                   0n25808            Show stacks

...

    0n153                                  0n7                Show stacks
    0n154                                  0n3                Show stacks
    0n156                                  0n29972            Show stacks
    0n159                                  0n4294959128       Show stacks
    0n160                                  0n30892            Show stacks
    0n161                                  0n136              Show stacks
    0n162                                  0n4294951910       Show stacks
    0n163                                  0n30892            Show stacks
    0n164                                  0n136              Show stacks
    0n167                                  0n4294965996       Show stacks

    Include inactive tags
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)

 

 






