---
title: COPP ビデオのミニポート ドライバー閉じるテンプレート コード
description: COPP ビデオのミニポート ドライバー閉じるテンプレート コード
ms.assetid: a7b088d6-a6cd-479d-b256-04def1de1736
keywords:
- COPP DirectX VA デバイス オブジェクトを解放します。
- COPP DirectX VA デバイス オブジェクトを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38110cb52cb8e963d4a5179e21f66657db0d0d10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556604"
---
# <a name="copp-video-miniport-driver-close-template-code"></a>COPP ビデオのミニポート ドライバー閉じるテンプレート コード


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

 

 





