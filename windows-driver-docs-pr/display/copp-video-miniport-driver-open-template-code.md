---
title: COPP ビデオのミニポート ドライバー テンプレートを開くコード
description: COPP ビデオのミニポート ドライバー テンプレートを開くコード
ms.assetid: 41facdef-c5f7-42f1-a251-07e4685649de
keywords:
- COPP DirectX VA デバイス オブジェクトを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b69898c84de240a53df5d241a90baacb4d25564
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531780"
---
# <a name="copp-video-miniport-driver-open-template-code"></a>COPP ビデオのミニポート ドライバー テンプレートを開くコード


## <span id="ddk_copp_video_miniport_driver_open_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_OPEN_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次のコード例を使用すると、デバイス オブジェクト COPP DirectX VA のインスタンスを作成できます。

```cpp
VP_STATUS
IoctlCOPPOpenDevice(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    ULONG uDevID = *(ULONG*)pInBuff->InputBuffer;
    COPP_DeviceData* pThis = VideoPortAllocatePool(pHwDeviceExtension,
                                              VpPagedPool,
                                              sizeof(COPP_DeviceData),
                                              &#39;PPOC&#39;);
    *pInBuff->ppThis = NULL;
    if (pThis == NULL) {
        *pInBuff->phr = ERROR_NOT_ENOUGH_MEMORY;
        return NO_ERROR;
    }
     *pInBuff->phr = COPPOpenVideoSession(pThis, uDevID);
    if (*pInBuff->phr == NO_ERROR) {
        *pInBuff->ppThis = pThis;
    }
    else {
        VideoPortFreePool(pHwDeviceExtension, pThis);
        *pInBuff->ppThis = NULL;
    }
    return NO_ERROR;
}
```

 

 





