---
title: タイムトラベルデバッグ拡張機能! 位置コマンド
description: '! 位置拡張には、現在のすべてのスレッド (現在の位置を含む) が表示されます。'
keywords:
- Windows のデバッグを配置する
ms.date: 09/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04651c8a9c416982720a15b7b3aa2d10bef3396
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916209"
---
# <a name="positions"></a>! 位置

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png) 

**! 位置**拡張は、タイムトラベルトレースの現在の位置を含む、すべてのアクティブなスレッドを表示します。

```dbgcmd
!positions 
```

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメータ

なし

## <a name="example"></a>例

この出力は、4つのスレッドを示しています。 スレッド3824は、左側の列の **>** によって示される現在のスレッドです。

```dbgcmd
0:000> !positions
>Thread ID=0x3824 - Position: F:0
 Thread ID=0x2684 - Position: A5:0
 Thread ID=0x2478 - Position: 200:0
 Thread ID=0x2DC4 - Position: 401:0
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-拡張コマンド](time-travel-debugging-extension-commands.md)