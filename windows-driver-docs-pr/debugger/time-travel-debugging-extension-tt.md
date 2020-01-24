---
title: タイムトラベルデバッグ拡張機能! tt コマンド
description: 時間を前後に移動できる! tt time トラベルデバッガー拡張機能。
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6af058ee25e25ee1875beb3a94005d526f895860
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706947"
---
# <a name="tt-time-travel"></a>! tt (タイムトラベル)

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

時間を前後に移動できるようにする、! tt (タイムトラベル) デバッガー拡張機能。

## <a name="tt-navigation-commands"></a>! tt ナビゲーションコマンド

! Tt 拡張機能を使用して、トレース内の特定の位置に移動することにより、時間の前後に移動します。 

```dbgcmd
!tt [position]
```

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメータ

**position**

その時点に移動するには、次のいずれかの形式で時刻の位置を指定します。
           
- {Position} が0から100までの10進数である場合、トレースに約そのパーセント移動します。 たとえば次のようになります。
    - ! tt 0-トレースの先頭への時刻の移動
    - ! tt 50-トレースを通じて中間に時間を移動する
    - ! tt 100-トレースの終わりまでの時間
 

- {Position} が #: # の場合 (# は16進数)、その位置に移動します。 の後の数値が省略されている場合、既定値は0になります。
    - ! tt 1A0:-位置1A0 に移動します: 0
    - ! tt 1A0: 0-位置1A0 に移動: 0
    - ! tt 1A0: 12F-位置 1A0: 12F に移動


   > [!NOTE]
   > トレースでは、12:0 など、トレース内の特定の位置参照を参照する2つの部分で構成される命令位置が使用されます。 または15:7。 2つの要素は、ここで説明するように定義された16進数です。
   >
   > xx: yy
   > 
   > xx-最初の要素はシーケンス番号で、シーケンス処理イベントに対応します。
   >
   > yy-2 番目の要素はステップ数で、シーケンスイベントからの命令数にほぼ対応します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
