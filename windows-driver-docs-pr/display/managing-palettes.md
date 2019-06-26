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
ms.openlocfilehash: d4cdbd9a79ed9f292f798997d81c91441e323a21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383431"
---
# <a name="managing-palettes"></a>パレットの管理


## <span id="ddk_managing_palettes_gg"></span><span id="DDK_MANAGING_PALETTES_GG"></span>


グラフィック ドライバーの管理作業の GDI サポートで「します。 ドライバーは、既定で GDI パレットを指定する必要があります、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo) GDI 関数を呼び出すときに[ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)します。 この時点で、ドライバーは、GDI サービスの関数の呼び出しで既定のパレットを作成する必要があります[ **EngCreatePalette**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)します。

設定可能なパレットをサポートするドライバーもサポートする必要があります、 [ **DrvSetPalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)関数。 この関数は、ディスプレイ ドライバーによって排他的に使用されます。

 

 





