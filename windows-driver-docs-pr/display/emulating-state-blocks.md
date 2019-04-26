---
title: 状態ブロックのエミュレート
description: 状態ブロックのエミュレート
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- WDK の表示状態のブロックをエミュレートします。
- 状態ブロック エミュレーション WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65f26d3c9d7ee83971f0fa6893b6f5c88c1e49ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355363"
---
# <a name="emulating-state-blocks"></a>状態ブロックのエミュレート


状態のブロックをエミュレートするために、マイクロソフトの Direct3D ランタイムを有効にするのには、次のように、レジストリを構成できます。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**注**  ランタイムでは、ユーザー モードのディスプレイ ドライバーの呼び出しません Direct3D ランタイムによって状態ブロックのエミュレーションを有効にするレジストリを構成すると後、 [**ステート セット**](https://msdn.microsoft.com/library/windows/hardware/ff569730)状態ブロック情報を設定する関数。

 

 

 





