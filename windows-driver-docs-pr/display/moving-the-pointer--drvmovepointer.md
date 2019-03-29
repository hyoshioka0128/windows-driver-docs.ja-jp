---
title: ポインター DrvMovePointer の移動
description: ポインター DrvMovePointer の移動
ms.assetid: cd82cea8-a37e-4e00-9342-9d6491e8c83c
keywords:
- 描画ポインター WDK Windows 2000 を表示します。
- ディスプレイ ドライバー WDK Windows 2000 では、ポインター
- Windows 2000 の WDK のポインターを表示します。
- DrvMovePointer
- ポインターの位置を移動
- ポインターを再配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f573774db34ab9e43efdd83b20da36563ed870b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580974"
---
# <a name="moving-the-pointer-drvmovepointer"></a>ポインターの移動: DrvMovePointer


## <span id="ddk_moving_the_pointer_drvmovepointer_gg"></span><span id="DDK_MOVING_THE_POINTER_DRVMOVEPOINTER_GG"></span>


場合[ **DrvSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff556289)し、ドライバーに含まれている[ **DrvMovePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff556248)もサポートされている必要があります。 この関数は、新しい位置に、ドライバーで管理されたポインターを移動します。 GDI はポインターの関数への呼び出しをシリアル化のため*DrvMovePointer*は呼び出さない、ディスプレイ ドライバーが任意のスレッドの描画中にしない限り、GCAPS\_ASYNCMOVE フラグが設定されている、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)構造体。

ドライバーを呼び出す必要があります[ **EngMovePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff564977) GDI のデバイスで、エンジンに管理されたポインターを移動します。 ドライバーは、GDI が呼び出すことによって、カーソルを管理することを要求[ **EngSetPointerShape**](https://msdn.microsoft.com/library/windows/hardware/ff565017)します。

 

 





