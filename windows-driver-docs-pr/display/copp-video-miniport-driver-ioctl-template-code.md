---
title: COPP ビデオ ミニポート ドライバーの IOCTL テンプレート コード
description: COPP ビデオ ミニポート ドライバーの IOCTL テンプレート コード
ms.assetid: 55a77261-016e-4ba6-8cb6-c45171759035
keywords:
- Ioctl WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54c1ad324a084c41fe871ef9bc2877149abc82ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839780"
---
# <a name="copp-video-miniport-driver-ioctl-template-code"></a>COPP ビデオ ミニポート ドライバーの IOCTL テンプレート コード


## <span id="ddk_copp_video_miniport_driver_ioctl_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_IOCTL_TEMPLATE_CODE_GG"></span>


このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

ビデオミニポートドライバーは、ディスプレイドライバーで発生した i/o 要求を処理するために、 [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数を実装する必要があります。 次のコード例は、ビデオミニポートドライバーが COPP Ioctl を処理する方法のみを示しています。

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

 

 





