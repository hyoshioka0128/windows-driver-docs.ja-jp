---
title: 24 fps のビデオ コンテンツを再生するための適応更新
description: Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーは、60 Hz のモニターで 24 フレームあたり 2 つ目の (fps) のビデオ コンテンツを再生するときに電源を節約するために、48 Hz アダプティブ更新を実装する必要があります。
ms.assetid: CFA1AE0F-B591-4C5E-A97B-8D4E4B475167
ms.date: 10/19/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: bb0ac9cacd5d61e254dc84f88b1af1a38b401c9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341578"
---
# <a name="adaptive-refresh-for-playing-24-fps-video-content"></a>24 fps のビデオ コンテンツを再生するための適応更新


Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーは、60 Hz のモニターで 24 フレームあたり 2 つ目の (fps) のビデオ コンテンツを再生するときに電源を節約するために、48 Hz アダプティブ更新を実装する必要があります。 このシナリオでは、モニターは 60 Hz から 24 fps ビデオ コンテンツを再生する 48 Hz のリフレッシュ レートに切り替わります。



## <a name="adaptive-refresh-reference"></a>アダプティブ更新参照

これらは、デバイス ドライバー インターフェイス (Ddi) WDDM 1.3 およびそれ以降のドライバーが 24 fps の再生に実装する必要があります。

これらの参照トピックには、ドライバーでこの機能を実装する方法について説明します。

-   [**D3DDDIARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddiarg_checkpresentdurationsupport) 
-   [**DXGI\_DDI\_ARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport) 
-   [**DXGKARG\_SETVIDPNSOURCEADDRESS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddress) (**期間**メンバー)
-   [**DXGKARG\_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay) (**期間**メンバー)
-   [**D3DDDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (**pfnCheckPresentDurationSupport**関数ポインター)
-   [**DXGI1\_3\_DDI\_ベース\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (**pfnCheckPresentDurationSupport**関数ポインター)

以下は、48 Hz アダプティブ リフレッシュ レートをサポートするために Windows 表示 Driver Model (WDDM) 1.3 およびそれ以降のユーザー モード ドライバーが表示される関数を実装する必要があります。

-   [*CheckPresentDurationSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkpresentdurationsupport)
-   [*pfnCheckPresentDurationSupport(DXGI)*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport)




 

 





