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
ms.openlocfilehash: 4544bff4ad6a3c8763090253a399b956ea7be92a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372868"
---
# <a name="moving-the-pointer-drvmovepointer"></a>ポインターの移動: DrvMovePointer


## <span id="ddk_moving_the_pointer_drvmovepointer_gg"></span><span id="DDK_MOVING_THE_POINTER_DRVMOVEPOINTER_GG"></span>


場合[ **DrvSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)し、ドライバーに含まれている[ **DrvMovePointer** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)もサポートされている必要があります。 この関数は、新しい位置に、ドライバーで管理されたポインターを移動します。 GDI はポインターの関数への呼び出しをシリアル化のため*DrvMovePointer*は呼び出さない、ディスプレイ ドライバーが任意のスレッドの描画中にしない限り、GCAPS\_ASYNCMOVE フラグが設定されている、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体。

ドライバーを呼び出す必要があります[ **EngMovePointer** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer) GDI のデバイスで、エンジンに管理されたポインターを移動します。 ドライバーは、GDI が呼び出すことによって、カーソルを管理することを要求[ **EngSetPointerShape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape)します。

 

 





