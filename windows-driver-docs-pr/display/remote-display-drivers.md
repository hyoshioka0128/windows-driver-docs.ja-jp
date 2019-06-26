---
title: リモート ディスプレイ ドライバー
description: リモートのディスプレイ ドライバーは、Windows 2000 ミラー ドライバー モデルに基づいており、リモート セッションでデスクトップを表示するために使用します。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9004d7a0d53ff2ac5438e8d41e27b2580a44ab0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386441"
---
# <a name="remote-display-drivers"></a>リモート ディスプレイ ドライバー


A*リモート ディスプレイ ドライバー*は Windows 2000 に基づいて[ミラー ドライバー](mirror-drivers.md)モデル、リモート セッションでデスクトップを表示するために使用されます。

正常にインストールして、Windows 8 以降を実行、リモート ディスプレイ ドライバーはのみ、次のデバイス ドライバー インターフェイス (Ddi) とを実装する必要があります。

-   [**DrvAssertMode**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)
-   [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)
-   [**DrvCompletePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)
-   [**DrvCopyBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)
-   [**DrvDisableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)
-   [**DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)
-   [**DrvDisableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)
-   [**DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)
-   [**DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)
-   [**DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)
-   [**DrvGetModes**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes)
-   [**DrvMovePointer**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)
-   [**DrvResetPDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvresetpdev)
-   [**DrvSetPointerShape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)

 

 





