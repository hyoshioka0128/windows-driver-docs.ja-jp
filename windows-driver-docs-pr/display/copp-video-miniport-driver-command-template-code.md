---
title: COPP ビデオ ミニポート ドライバーのコマンド テンプレート コード
description: COPP ビデオ ミニポート ドライバーのコマンド テンプレート コード
ms.assetid: a772fc78-0024-4834-8ff3-a1cf6672b316
keywords:
- WDK COPP コマンド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685c20c7ccf515fe5879790694e94346839e268e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342986"
---
# <a name="copp-video-miniport-driver-command-template-code"></a>COPP ビデオ ミニポート ドライバーのコマンド テンプレート コード


## <span id="ddk_copp_video_miniport_driver_command_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_COMMAND_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

COPP DirectX VA デバイス オブジェクトの操作を実行するのにには、次のコード例を使用します。

```cpp
VP_STATUS
IoctlCOPPCommand(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPCommand* lpin = (DXVA_COPPCommand*)pInBuff->InputBuffer;
     *pInBuff->phr = COPPCommand(pThis, lpin);
    return NO_ERROR;
}
```

 

 





