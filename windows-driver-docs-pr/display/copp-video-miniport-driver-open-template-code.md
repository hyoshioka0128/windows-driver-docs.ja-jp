---
title: COPP ビデオ ミニポート ドライバーの開始テンプレート コード
description: COPP ビデオ ミニポート ドライバーの開始テンプレート コード
ms.assetid: 41facdef-c5f7-42f1-a251-07e4685649de
keywords:
- COPP DirectX VA デバイス オブジェクトを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b2dc452c4c889dd13c0e48f7e7aaa0ebed0abfa
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350367"
---
# <a name="copp-video-miniport-driver-open-template-code"></a>COPP ビデオ ミニポート ドライバーの開始テンプレート コード


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
                                              'PPOC');
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

 

 





