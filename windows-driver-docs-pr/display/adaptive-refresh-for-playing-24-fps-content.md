---
title: 24 fps ビデオコンテンツを再生するためのアダプティブ更新
description: Windows Display Driver Model (WDDM) 1.3 以降のドライバーが 60 Hz モニターで24フレーム/秒 (fps) ビデオコンテンツを再生する場合、電力を節約するには 48 Hz アダプティブリフレッシュを実装する必要があります。
ms.assetid: CFA1AE0F-B591-4C5E-A97B-8D4E4B475167
ms.date: 10/19/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 65c97ff83ae5382c87c84ae2ac6cd9d0798ab791
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839834"
---
# <a name="adaptive-refresh-for-playing-24-fps-video-content"></a>24 fps ビデオコンテンツを再生するためのアダプティブ更新


Windows Display Driver Model (WDDM) 1.3 以降のドライバーが 60 Hz モニターで24フレーム/秒 (fps) ビデオコンテンツを再生する場合、電力を節約するには 48 Hz アダプティブリフレッシュを実装する必要があります。 このシナリオでは、モニターは 60 Hz から 48 Hz のリフレッシュレートに切り替わり、24 fps のビデオコンテンツを再生します。



## <a name="adaptive-refresh-reference"></a>アダプティブ更新のリファレンス

これらは、デバイスドライバーインターフェイス (DDIs) であり、WDDM 1.3 以降のドライバーで 24 fps 再生用に実装する必要があります。

これらの参照トピックでは、ドライバーにこの機能を実装する方法について説明します。

-   [**D3DDDIARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_checkpresentdurationsupport) 
-   [**DXGI\_DDI\_ARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport) 
-   [**Dxgkarg\_SETVIDPNSOURCEADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddress) (**Duration**メンバー)
-   [**Dxgkarg\_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay) (**Duration**メンバー)
-   [**D3DDDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (**pfnCheckPresentDurationSupport**関数ポインター)
-   [**DXGI1\_3\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (**pfnCheckPresentDurationSupport**関数ポインター)

次に示すのは、48 Hz のアダプティブリフレッシュ率をサポートするために、Windows Display Driver Model (WDDM) 1.3 以降のユーザーモード表示ドライバーが実装する必要がある関数です。

-   [*CheckPresentDurationSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkpresentdurationsupport)
-   [*pfnCheckPresentDurationSupport (DXGI)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport)




 

 





