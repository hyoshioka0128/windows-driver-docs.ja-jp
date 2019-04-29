---
title: デバッグ拡張機能の移動をタイム! tt コマンド
description: '! 時間で前方と後方を移動することができます tt タイム トラベル デバッガー拡張します。'
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26817ac6f106064afdec8f80a74359c23d476768
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389118"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

#  <a name="tt-time-travel"></a>! tt (タイム トラベル)

! Tt (タイム トラベル) デバッガー拡張機能を時間で前方と後方を移動することができます。

## <a name="tt-navigation-commands"></a>! tt ナビゲーション コマンド

使用して、! tt の拡張機能は、時間で前方または後方は、トレース内の指定位置に移動して移動します。 

```dbgcmd
!tt [position] 
```

## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメーター

**position**

時間の点に移動する次の形式のいずれかの時間位置を指定します。
           
- {0} 位置} が 0 から 100 までの 10 進数である場合は、トレースに約その % に移動します。 次に、例を示します。
    - ! ttdext.tt 0 - 時間は、トレースの先頭に移動
    - ! ttdext.tt 50 - タイム トラベルに途中で、トレースを通じて
    - ! トレースの最後に、ttdext.tt 100 - タイム トラベル
 

- {0} 位置} が # である場合: #, # は、16 進数、送信するときにその位置にします。 数値の場合: は省略すると、既定値は 0。
    - ! ttdext.tt 1A0:-1A0:0 位置への移動をタイム
    - ! ttdext.tt 1A0:0 - タイム トラベル 1A0:0 を配置するには
    - ! ttdext.tt 1A0:12F - タイム トラベル 1A0:12F を配置するには


   > [!NOTE]
   > トレースは、たとえば 12:0 では、トレース内の特定の位置の参照を参照する 2 つの部分の命令の位置を使用します。 または、15:7。 2 つの要素は、前述のように定義されている 16 進の番号です。
   >
   > xx:yy
   > 
   > xx - 最初の要素は、シーケンス処理イベントに対応するシーケンス番号です。
   >
   > yy - 2 番目の要素は、シーケンス処理のイベント以降、命令数にほぼ対応する手順数です。


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のみの動作時間は、トレースを移動します。 タイム トラベルの詳細については、次を参照してください。[時出張デバッグ - 概要](time-travel-debugging-overview.md)します。

## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---






