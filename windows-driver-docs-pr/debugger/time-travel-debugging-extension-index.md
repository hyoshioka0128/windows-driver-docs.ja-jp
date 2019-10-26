---
title: タイムトラベルデバッグ拡張機能! index コマンド
description: '! インデックス拡張インデックスは、タイムトラベルをトレースしたり、インデックスの状態情報を表示したりします。'
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 044410ba9e7ac93c2f27c589a8f30bfb00d95d9a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916214"
---
#  <a name="index"></a>! インデックス

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

**! インデックス**拡張インデックスは、タイムトラベルをトレースしたり、インデックスの状態情報を表示したりします。

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
0:000> !tt.index -status
Index file loaded.
```
**-force**

読み込めないインデックスファイルがディスク上に存在する場合でも、`!index -force` を使用してトレースのインデックスを再作成します。

```dbgcmd
0:000> !tt.index -force
Successfully created the index in 152ms.
```


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-拡張コマンド](time-travel-debugging-extension-commands.md)
