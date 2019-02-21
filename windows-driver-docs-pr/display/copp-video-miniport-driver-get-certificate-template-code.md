---
title: COPP ビデオのミニポート ドライバー証明書テンプレート コードを取得
description: COPP ビデオのミニポート ドライバー証明書テンプレート コードを取得
ms.assetid: 13810013-389a-458d-be9d-e81a0b248dec
keywords:
- 証明書 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af62efe54b47df8359169fa80bd4a8197ca5ba70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558206"
---
# <a name="copp-video-miniport-driver-get-certificate-template-code"></a>COPP ビデオのミニポート ドライバー証明書テンプレート コードを取得


## <span id="ddk_copp_video_miniport_driver_get_certificate_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_GET_CERTIFICATE_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次のコード例を使用して、サイズ、COPP DirectX VA デバイス オブジェクトのグラフィックス ハードウェアの証明書のバイト単位で取得します。

```cpp
VP_STATUS
IoctlCOPPGetCertificateLength(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    HRESULT* phr = pInBuff->phr;
     *phr = COPPGetCertificateLength(pThis, (ULONG*)pVideoRequestPacket->OutputBuffer);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = sizeof(ULONG);
    }
    return NO_ERROR;
}
```

 

 





