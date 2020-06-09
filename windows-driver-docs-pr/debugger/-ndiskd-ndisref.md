---
title: ndiskd ndisref
description: Ndisref 拡張機能は、追跡された参照カウントのデバッグログを表示します。
ms.assetid: 6860A567-1017-4184-B8DF-157467360FB9
keywords:
- ndisref Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisref
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d2856dc43389d6096bd818a0410d75a017672dd7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534189"
---
# <a name="ndiskdndisref"></a>!ndiskd.ndisref


**! Ndiskd**拡張機能は、追跡された参照カウントのデバッグログを表示します。

```console
!ndiskd.ndisref [-handle <x>] [-tagtype <str>] [-stacks] [-tag <str>] [-refdebug] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 Refcount ブロックのハンドル。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span>*-tagtype*   
タグの列挙型。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span>*-stacks*   
スタックトレースが含まれます (使用可能な場合)。

<span id="_______-tag______"></span><span id="_______-TAG______"></span>*-タグ*   
制限は1つのタグに表示されます。

<span id="_______-refdebug______"></span><span id="_______-REFDEBUG______"></span>*-refdebug*   
使用可能な場合は詳細なデバッグログを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

次の例では、NDIS ミニポートドライバーのハンドルを **! ndiskd ndisref**拡張機能に渡して、そのドライバーの refcount ブロックを表示します。 まず、システム上のすべてのミニポートドライバーの一覧を表示するには、パラメーターを付けずに[**ミニドライバー**](-ndiskd-minidriver.md)を実行します。 次の出力例では、kdnic ドライバーのハンドルである ffffdf801418d650 を探します。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

ミニポートドライバーのハンドルを使用して、 **! ndiskd ndisref**コマンドを入力して、このミニポートドライバーの refcount ブロックを確認します。 次の例では、簡潔にするために refcount ブロックの excised を使用しています。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)

 

 






