---
title: COPP ビデオ ミニポート ドライバーの終了テンプレート コード
description: COPP ビデオ ミニポート ドライバーの終了テンプレート コード
ms.assetid: a7b088d6-a6cd-479d-b256-04def1de1736
keywords:
- COPP DirectX VA デバイス オブジェクトを解放します。
- COPP DirectX VA デバイス オブジェクトを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38110cb52cb8e963d4a5179e21f66657db0d0d10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342971"
---
# <a name="copp-video-miniport-driver-close-template-code"></a>COPP ビデオ ミニポート ドライバーの終了テンプレート コード


## <span id="ddk_copp_video_miniport_driver_close_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_CLOSE_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

COPP DirectX VA デバイス オブジェクトのインスタンスを解放するのにには、次のコード例を使用します。

```cpp
VP_STATUS
IoctlCOPPCloseDevice(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
     *pInBuff->phr = COPPCloseVideoSession(pThis);
    VideoPortFreePool(pHwDeviceExtension, pThis);
    *pInBuff->ppThis = NULL;
    return NO_ERROR;
}
```

 

 





