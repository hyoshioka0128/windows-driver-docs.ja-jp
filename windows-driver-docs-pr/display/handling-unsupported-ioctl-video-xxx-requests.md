---
title: サポートされていない IOCTL_VIDEO_XXX 要求の処理
description: サポートされていない IOCTL_VIDEO_XXX 要求の処理
ms.assetid: e3a96cc2-bb7f-4060-bf71-d8a63b918329
keywords:
- ビデオミニポートドライバー WDK Windows 2000、要求の処理
- 要求処理 WDK ビデオミニポート
- サポートされていない IOCTL_VIDEO_XXX 要求 WDK ビデオミニポート
- IOCTL_VIDEO_XXX が WDK ビデオミニポートを要求する
- I/o WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052b6cc23759a7c3dc32755c8b76138a30f73e3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839655"
---
# <a name="handling-unsupported-ioctl_video_xxx-requests"></a>サポートされていない IOCTL\_ビデオ\_XXX 要求の処理


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


また、 [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)の各関数は、次のように、サポートされていない IOCTL\_VIDEO\_*XXX*の受信を処理する必要があります。

1.  Input VRP の**Status**フィールドを ERROR\_無効な\_関数に設定します。

2.  入力 VRP の**情報**フィールドをゼロに設定します。

3.  要求が処理されたことを示す**場合は TRUE**を返します。

詳細については、[**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)と[**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_status_block)構造体を参照してください。

 

 





