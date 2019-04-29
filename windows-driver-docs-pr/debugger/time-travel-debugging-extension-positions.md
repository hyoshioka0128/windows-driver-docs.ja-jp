---
title: デバッグ拡張機能の移動をタイム! コマンドの配置
description: '! 位置の拡張機能がアクティブなすべてのスレッドを現在の位置を含むを表示します。'
keywords:
- Windows デバッグ位置
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 036d7057fefec0a39780ddad259079c81ac73605
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327070"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png) 

# <a name="positions"></a>! 位置


**! 位置**拡張機能がアクティブなすべてのスレッドをタイム トラベルのトレースで現在の位置を含むを表示します。


```dbgcmd
!positions 
```


## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメーター

なし


## <a name="example"></a>例

この出力は、4 つのスレッドを示しています。 3824 は現在のスレッドによって示される**>** 左の列にします。

```dbgcmd
0:000> !positions
>Thread ID=0x3824 - Position: F:0
 Thread ID=0x2684 - Position: A5:0
 Thread ID=0x2478 - Position: 200:0
 Thread ID=0x2DC4 - Position: 401:0
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のみの動作時間は、トレースを移動します。 タイム トラベルの詳細については、次を参照してください。[時出張デバッグ - 概要](time-travel-debugging-overview.md)します。


## <a name="see-also"></a>参照

[時間の移動 [デバッグ] - 拡張機能のコマンド](time-travel-debugging-extension-commands.md)


 

 





