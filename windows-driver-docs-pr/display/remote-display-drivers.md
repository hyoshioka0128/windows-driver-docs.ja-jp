---
title: リモート ディスプレイ ドライバー
description: リモートのディスプレイ ドライバーは、Windows 2000 ミラー ドライバー モデルに基づいており、リモート セッションでデスクトップを表示するために使用します。
ms.assetid: 249528D3-B5F1-41D8-86BF-B9DC623FB480
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bd8ff555fc190468902e2b35c285e64eaf91578
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378436"
---
# <a name="remote-display-drivers"></a>リモート ディスプレイ ドライバー


A*リモート ディスプレイ ドライバー*は Windows 2000 に基づいて[ミラー ドライバー](mirror-drivers.md)モデル、リモート セッションでデスクトップを表示するために使用されます。

正常にインストールして、Windows 8 以降を実行、リモート ディスプレイ ドライバーはのみ、次のデバイス ドライバー インターフェイス (Ddi) とを実装する必要があります。

-   [**DrvAssertMode**](https://msdn.microsoft.com/library/windows/hardware/ff556178)
-   [**DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)
-   [**DrvCompletePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556181)
-   [**DrvCopyBits**](https://msdn.microsoft.com/library/windows/hardware/ff556182)
-   [**DrvDisableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556196)
-   [**DrvDisablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556198)
-   [**DrvDisableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556200)
-   [**DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)
-   [**DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)
-   [**DrvEscape**](https://msdn.microsoft.com/library/windows/hardware/ff556217)
-   [**DrvGetModes**](https://msdn.microsoft.com/library/windows/hardware/ff556233)
-   [**DrvMovePointer**](https://msdn.microsoft.com/library/windows/hardware/ff556248)
-   [**DrvResetPDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556276)
-   [**DrvSetPointerShape**](https://msdn.microsoft.com/library/windows/hardware/ff556289)

 

 





