---
title: タイムトラベルデバッグ拡張機能! 位置コマンド
description: '! 位置拡張には、現在のすべてのスレッド (現在の位置を含む) が表示されます。'
keywords:
- Windows のデバッグを配置する
ms.date: 01/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8e93a42646d0fb6c22901607f3dba4eed0a692ed
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706969"
---
# <a name="positions"></a>! 位置

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png) 

**! 位置**拡張は、タイムトラベルトレースの現在の位置を含む、すべてのアクティブなスレッドを表示します。

```dbgcmd
!positions
```

## <a name="span-idddk__analyze_dbgspanspan-idddk__analyze_dbgspanparameters"></a><span id="ddk__analyze_dbg"></span><span id="DDK__ANALYZE_DBG"></span>パラメータ

None

## <a name="example"></a>例

この出力は5つのスレッドを示しています。 スレッド1660は、左側の列の **>** によって示される現在のスレッドです。

```dbgcmd
0:000> !positions
>*Thread ID=0x1660 - Position: 724:0
  Thread ID=0x3E6C - Position: A8B:0
  Thread ID=0x30EC - Position: A8A:0
  Thread ID=0x1F40 - Position: A8E:0
  Thread ID=0x4170 - Position: C44:0
* indicates an actively running thread
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

ttdext

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

[タイムトラベルデバッグ-拡張コマンド](time-travel-debugging-extension-commands.md)