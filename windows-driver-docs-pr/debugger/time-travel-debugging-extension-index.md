---
title: デバッグ拡張機能の移動をタイム! コマンドのインデックス
description: '! タイム トラベル トレースまたはインデックスの状態情報を表示拡張機能のインデックスのインデックスを作成します。'
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e5b6875e29a47074688c39d1398e121607f107aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551039"
---
#  <a name="index"></a>! インデックス

![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

**! インデックス**インデックス タイム トラベルの拡張機能は、トレースまたはインデックスの状態情報が表示されます。

```dbgsyntax
!index [-status] [-force] 
```


使用`!index`現在のトレースでインデックス作成のパスを実行するためです。 

```dbgcmd
0:000> !index
Indexed 10/14 keyframes
Indexed 14/14 keyframes
Successfully created the index in 535ms.
```

現在のトレースが既にインデックス化されている場合、! index コマンドは、何も行われません。

```dbgcmd
0:000> !index
Successfully created the index in 0ms.
```



## <a name="span-idddkanalyzedbgspanspan-idddkanalyzedbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメーター

**-状態**

使用`!index -status`トレース インデックスの状態を報告します。

```dbgcmd
0:000> !tt.index -status
Index file loaded.
```
**-強制**

使用`!index -force`に読み込めないインデックス ファイルがディスク上に存在する場合でも、トレースを再作成します。

```dbgcmd
0:000> !tt.index -force
Successfully created the index in 152ms.
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のみの動作時間は、トレースを移動します。 タイム トラベルの詳細については、次を参照してください。[時出張デバッグ - 概要](time-travel-debugging-overview.md)します。


## <a name="see-also"></a>参照

[時間の移動 [デバッグ] - 拡張機能のコマンド](time-travel-debugging-extension-commands.md)


-------

 





