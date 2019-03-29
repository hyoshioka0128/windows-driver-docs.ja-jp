---
title: ディスプレイ ドライバーでの複数モニターのサポート
description: ディスプレイ ドライバーでの複数モニターのサポート
ms.assetid: ba15af67-94c0-4c37-8b3d-b1472e731d88
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、複数のモニター
- 複数のモニター WDK
- マルチ モニター システム WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1670b1715e7c668f1417648d6da412bbe3ef9ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573745"
---
# <a name="multiple-monitor-support-in-the-display-driver"></a>ディスプレイ ドライバーでの複数モニターのサポート


## <span id="ddk_multiple_monitor_support_in_the_display_driver_gg"></span><span id="DDK_MULTIPLE_MONITOR_SUPPORT_IN_THE_DISPLAY_DRIVER_GG"></span>


Windows 2000 以降では、マルチ モニターのサポートが提供されます。そのため、ドライバーの記述者を表示する必要がありますこのサポートを提供する特別なコードを実装していません。

グローバル変数を使用せず、ディスプレイ ドライバーを実装する必要があります。 すべての状態が存在する必要があります、 *PDEV*の特定のディスプレイ ドライバー。 GDI は呼び出す[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)ビデオのミニポート ドライバーによって作成されるすべてのハードウェアのデバイスの拡張機能用です。

マルチ モニター システムでウィンドウの変更を追跡するために、ドライバーは、デスクトップ座標で WNDOBJ オブジェクトを作成する GDI を要求できます。 ドライバーは呼び出すことによって[ **EngCreateWnd** ](https://msdn.microsoft.com/library/windows/hardware/ff564769) WO フラグを使用して\_RGN\_デスクトップ\_座標系。 参照してください[ウィンドウの変更を追跡](tracking-window-changes.md)詳細についてはします。

マルチ モニター システムでは、GDI が内のデバイスのデスクトップの位置を格納、 **dmPosition**のメンバー、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体。

 

 





