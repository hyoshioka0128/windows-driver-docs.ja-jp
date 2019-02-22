---
title: COPP ビデオのミニポート ドライバー IOCTL テンプレート コード
description: COPP ビデオのミニポート ドライバー IOCTL テンプレート コード
ms.assetid: 55a77261-016e-4ba6-8cb6-c45171759035
keywords:
- Ioctl WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fbf14e5ffb345417be42fd1d0d375267f35718
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538645"
---
# <a name="copp-video-miniport-driver-ioctl-template-code"></a>COPP ビデオのミニポート ドライバー IOCTL テンプレート コード


## <span id="ddk_copp_video_miniport_driver_ioctl_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_IOCTL_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

ビデオのミニポート ドライバーを実装する必要があります、 [ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)ディスプレイ ドライバーで発生する I/O 要求を処理する関数。 次のコード例では、ビデオのミニポート ドライバーが COPP Ioctl を処理する方法のみを示しています。

```cpp
BOOLEAN
HwVidStartIO(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    VP_STATUS vpStatus;
    switch (pVideoRequestPacket->IoControlCode)
    {
        case IOCTL_COPP_OpenDevice:
            vpStatus = IoctlCOPPOpenDevice(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_GetCertificateLength:
            vpStatus = IoctlCOPPGetCertificateLength(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_KeyExchange:
            vpStatus = IoctlCOPPKeyExchange(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_StartSequence:
            vpStatus = IoctlCOPPStartSeqence(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_Command:
            vpStatus = IoctlCOPPCommand(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_Status:
            vpStatus = IoctlCOPPStatus(pHwDeviceExtension, pVideoRequestPacket);
            break;
        case IOCTL_COPP_CloseDevice:
            vpStatus = IoctlCOPPCloseDevice(pHwDeviceExtension, pVideoRequestPacket);
            break;
        default:
            vpStatus = ERROR_INVALID_FUNCTION;
            break;
    }
    pVideoRequestPacket->StatusBlock->Status = vpStatus;
    return TRUE;
}
```

 

 





