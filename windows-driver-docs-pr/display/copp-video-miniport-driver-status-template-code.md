---
title: COPP ビデオのミニポート ドライバーの状態のテンプレート コード
description: COPP ビデオのミニポート ドライバーの状態のテンプレート コード
ms.assetid: 4d0d0f95-8a21-4863-9930-ddee7d944c04
keywords:
- WDK COPP のステータス情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f59194f385daa93503174b640e6a7f71b56ad9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558058"
---
# <a name="copp-video-miniport-driver-status-template-code"></a>COPP ビデオのミニポート ドライバーの状態のテンプレート コード


## <span id="ddk_copp_video_miniport_driver_status_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_STATUS_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次のコード例を使用すると、COPP DirectX VA デバイス オブジェクトに関連付けられている保護されたビデオ セッションの状態を取得できます。

```cpp
VP_STATUS
IoctlCOPPStatus(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPStatusInput* lpin = (DXVA_COPPStatusInput*)pInBuff->InputBuffer;
    DXVA_COPPStatusOutput* lpout = (DXVA_COPPStatusOutput*)pVideoRequestPacket->OutputBuffer;
    HRESULT* phr = pInBuff->phr;
     *phr =  COPPQueryStatus(pThis, lpin, lpout);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = sizeof(DXVA_COPPStatusOutput);
    }
    return S_OK;
}
```

 

 





