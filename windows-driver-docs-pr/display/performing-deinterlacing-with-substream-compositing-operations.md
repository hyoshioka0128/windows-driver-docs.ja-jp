---
title: サブストリーム合成の操作でデインター レースを実行します。
description: サブストリーム合成操作によるデインターレースの実行
ms.assetid: e6759e88-5cbb-4372-8a92-312f1684b99d
keywords:
- デインター レース WDK DirectX va なので、サブストリームの合成を組み合わせること
- 結合サブストリームの合成 WDK DirectX VA
- サブストリームの合成 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c0066539556c05b2863c5b3f5eedf3a7ccef96bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385577"
---
# <a name="performing-deinterlacing-with-substream-compositing-operations"></a>サブストリーム合成操作によるデインターレースの実行

**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

次のコード例を使用すると、ビデオ ストリームの上にビデオ ストリームと合成ビデオ サブストリーム デインター レースを結合する演算を実行できます。 コード例の実装、 [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数。 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)コールバック関数へのポインターを構造体します。 この例のコードのみは*DdMoCompRender*サブストリーム合成の操作でデインター レースを使用します。 実装について*DdMoCompRender* ProcAmp コントロールを実行して、操作をデインター レースを参照してください[ProcAmp コントロールを実行して操作のデインター レース](performing-procamp-control-and-deinterlacing-operations.md)します。

```cpp
DWORD APIENTRY
MOCOMPCB_RENDER(PDD_RENDERMOCOMPDATA lpData)
{
  // The driver saves the device class object in lpDriverReserved1 
   // during the DdMoCompCreate callback. For more information, 
   // see Creating Instances of DirectX VA Device Objects.
 DXVA_DeviceBaseClass* pDXVABase =
         (DXVA_DeviceBaseClass*)lpData->lpMoComp->lpDriverReserved1;
 if (pDXVABase == NULL) {
      lpData->ddRVal = E_POINTER;  
      return DDHAL_DRIVER_HANDLED;
  }
  switch (lpData->dwFunction) {
  case DXVA_DeinterlaceBltExFnCode:
 {  
      DXVA_DeinterlaceBobDeviceClass* pDXVADev =
                        (DXVA_DeinterlaceBobDeviceClass*)pDXVABase;
      DXVA_DeinterlaceBltEx* lpBlt = 
             (DXVA_DeinterlaceBltEx*)lpData->lpInputData;
      LPDDMOCOMPBUFFERINFO lpBuffInfo = lpData->BufferInfo;

      for (DWORD i = 0; i < lpBlt->NumSourceSurfaces; i++) {
          lpBlt->Source[i].lpDDSSrcSurface = 
                          lpBuffInfo[1 + i].lpCompSurface;
      }

       // Part of the Deinterlace DDI.
      lpData->ddRVal = pDXVADev->DeinterlaceBltEx(
                                       lpBlt->rtTarget,
                                       &lpBlt->rcTarget,
                                       lpBlt->BackgroundColor,
                                       lpBlt->DestinationFormat,
                                       lpBlt->DestinationFlags,
                                       lpBuffInfo[0].lpCompSurface,
                                       lpBlt->Source,
                                       lpBlt->NumSourceSurfaces,
                                       lpBlt->Alpha);
      return DDHAL_DRIVER_HANDLED;
  }
  default:
      lpData->ddRVal = E_INVALIDARG;
 return DDHAL_DRIVER_HANDLED;
  }

lpData->ddRVal = DDERR_CURRENTLYNOTAVAIL;
return DDHAL_DRIVER_HANDLED;
}
```

 

 





