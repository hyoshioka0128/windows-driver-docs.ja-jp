---
title: 状態ブロックのエミュレート
description: 状態ブロックのエミュレート
ms.assetid: 1ede9f1c-f5bb-4f41-8152-63d8663fd99e
keywords:
- WDK の表示状態のブロックをエミュレートします。
- 状態ブロック エミュレーション WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27b793b62b00370fe7ced6d88c138fa8111d81d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355213"
---
# <a name="emulating-state-blocks"></a>状態ブロックのエミュレート


状態のブロックをエミュレートするために、マイクロソフトの Direct3D ランタイムを有効にするのには、次のように、レジストリを構成できます。

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Direct3D
KeyValue  : EmulateStateBlocks
ValueType : REG_DWORD
ValueData : 1 for D3D runtime emulation of stateblocks, 0 for driver implementation (default).
```

**注**  ランタイムでは、ユーザー モードのディスプレイ ドライバーの呼び出しません Direct3D ランタイムによって状態ブロックのエミュレーションを有効にするレジストリを構成すると後、 [**ステート セット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_stateset)状態ブロック情報を設定する関数。

 

 

 





