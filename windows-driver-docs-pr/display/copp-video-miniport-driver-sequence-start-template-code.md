---
title: COPP ビデオ ミニポート ドライバーのシーケンス開始テンプレート コード
description: COPP ビデオ ミニポート ドライバーのシーケンス開始テンプレート コード
ms.assetid: f1fc0d03-43f6-44a0-b911-1ca473e4e701
keywords:
- シーケンスの先頭 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb5c9294e1b38975e75bb8c49c9328a38faf6de6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331326"
---
# <a name="copp-video-miniport-driver-sequence-start-template-code"></a>COPP ビデオ ミニポート ドライバーのシーケンス開始テンプレート コード


## <span id="ddk_copp_video_miniport_driver_sequence_start_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_SEQUENCE_START_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次のコード例を使用して、現在のビデオ セッション COPP DirectX VA デバイス オブジェクトの保護モードを設定します。

```cpp
VP_STATUS
IoctlCOPPStartSeqence(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    DXVA_COPPSignature* lpin = (DXVA_COPPSignature*)pInBuff->InputBuffer;
     *pInBuff->phr = COPPSequenceStart(pThis, lpin);
    return NO_ERROR;
}
```

 

 





