---
title: Time Travel Debugging Extension !index Command
description: The !index extension indexes time travel traces or displays index status information.
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: efde351e74b6ea40b3b27c8872459ff0adc9ca32
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706946"
---
# <a name="index"></a>!index

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

The **!index** extension indexes time travel traces or displays index status information.

```dbgsyntax
!index [-status] [-force]
```


現在のトレースに対してインデックス作成パスを実行するには、`!index` を使用します。 

```dbgcmd
0:000> !index
Indexed 10/14 keyframes
Indexed 14/14 keyframes
Successfully created the index in 535ms.
```

現在のトレースにインデックスが既に作成されている場合、! index コマンドでは何も実行されません。

```dbgcmd
0:000> !index
Successfully created the index in 0ms.
```



## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメータ

**-状態**

トレースインデックスの状態をレポートするには、`!index -status` を使用します。

```dbgcmd
0:000> index -status
Index file loaded.
```
**-force**

読み込めないインデックスファイルがディスク上に存在する場合でも、`!index -force` を使用してトレースのインデックスを再作成します。

```dbgcmd
0:000> index -force
Successfully created the index in 152ms.
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

[タイムトラベルデバッグ-拡張コマンド](time-travel-debugging-extension-commands.md)
