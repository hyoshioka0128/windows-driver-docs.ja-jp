---
title: パレットの管理
description: パレットの管理
ms.assetid: 7917b01f-f57d-4262-80b6-9e11e797e3b5
keywords:
- 色、GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、色
- WDK GDI の色の管理
- Windows 2000 の WDK のパレットを表示します。
- WDK の GDI や色の描画
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff45614ba2c715cb754b9491f8b918da57011758
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380399"
---
# <a name="managing-palettes"></a>パレットの管理


## <span id="ddk_managing_palettes_gg"></span><span id="DDK_MANAGING_PALETTES_GG"></span>


グラフィック ドライバーの管理作業の GDI サポートで「します。 ドライバーは、既定で GDI パレットを指定する必要があります、 [ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835) GDI 関数を呼び出すときに[ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)します。 この時点で、ドライバーは、GDI サービスの関数の呼び出しで既定のパレットを作成する必要があります[ **EngCreatePalette**](https://msdn.microsoft.com/library/windows/hardware/ff564212)します。

設定可能なパレットをサポートするドライバーもサポートする必要があります、 [ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)関数。 この関数は、ディスプレイ ドライバーによって排他的に使用されます。

 

 





