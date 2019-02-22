---
title: DirectX VA デバイスの取得
description: DirectX VA デバイスの取得
ms.assetid: 7af82243-7cb3-4e66-a6ee-3f4220baa459
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、デバイスの取得
- DirectX VA デバイスの取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2facbc48422e8f394f06defe29a51474d4b45c7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529362"
---
# <a name="retrieving-directx-va-devices"></a>DirectX VA デバイスの取得


## <span id="ddk_retrieving_directx_va_devices_gg"></span><span id="DDK_RETRIEVING_DIRECTX_VA_DEVICES_GG"></span>


次のコード例を使用すると、VA の DirectX デバイスを取得できます。 このコードは、の実装、 [ *DdMoCompGetGuids* ](https://msdn.microsoft.com/library/windows/hardware/ff550236)コールバック関数。 **GetMoCompGuids**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)コールバック関数へのポインターを構造体します。

```cpp
DWORD g_dwDXVANumSupportedGUIDs = 4;
const GUID* g_DXVASupportedGUIDs[4] = {
 &DXVA_DeinterlaceContainerDevice,
    &DXVA_ProcAmpControlDevice
    &DXVA_DeinterlaceBobDevice
 &DXVA_COPPDevice
};

DWORD APIENTRY
  MOCOMPCB_GETGUIDS(
    PDD_GETMOCOMPGUIDSDATA  lpData
    )
{
    DWORD dwNumToCopy;

    // If lpGuids == NULL, the driver must return the number of 
    // supported GUIDS in the dwNumGuids parameter. If non-NULL, 
    // the supported GUIDS must be copied into the buffer at lpGuids.
    if (lpData->lpGuids) {
        dwNumToCopy = min(g_dwDXVANumSupportedGUIDs, lpData->dwNumGuids);
        for (DWORD i = 0; i < dwNumToCopy; i++) {
            lpData->lpGuids[i] = *g_DXVASupportedGUIDs[i];
        }
    }
    else {
        dwNumToCopy = g_dwDXVANumSupportedGUIDs;
    }

    lpData->dwNumGuids = dwNumToCopy;
    lpData->ddRVal = DD_OK;

    return DDHAL_DRIVER_HANDLED;
}
```

 

 





