---
title: サポートされていない IOCTL_VIDEO_XXX 要求の処理
description: サポートされていない IOCTL_VIDEO_XXX 要求の処理
ms.assetid: e3a96cc2-bb7f-4060-bf71-d8a63b918329
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- サポートされていない IOCTL_VIDEO_XXX 要求 WDK ビデオ ミニポート
- IOCTL_VIDEO_XXX 要求 WDK のビデオのミニポート
- I/O WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9ae27c740f26e72a28d9a0f772dd0cb27cee0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369828"
---
# <a name="handling-unsupported-ioctlvideoxxx-requests"></a>処理のサポートされていない IOCTL\_ビデオ\_XXX 要求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


すべて[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)関数もサポートされていない IOCTL の確認メッセージを処理する必要があります\_ビデオ\_*XXX*、次のようにします。

1.  セットの入力 VRP の**状態**エラー フィールド\_無効な\_関数。

2.  セットの入力 VRP の**情報**フィールドをゼロにします。

3.  返す**TRUE**を要求の処理を示します。

参照してください、 [**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)と[**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_status_block)の構造体詳細についてはします。

 

 





