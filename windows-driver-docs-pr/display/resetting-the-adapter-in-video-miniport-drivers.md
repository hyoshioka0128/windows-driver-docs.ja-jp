---
title: ビデオ ミニポート ドライバーでのアダプターのリセット
description: ビデオ ミニポート ドライバーでのアダプターのリセット
ms.assetid: 321a5b6c-5a70-4acb-bf88-42ffb0cff86d
keywords:
- ビデオミニポートドライバー WDK Windows 2000、アダプターのリセット
- アダプターのリセット WDK ビデオミニポート
- HwVidResetHw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9dc09cea231eed909af354190c9b94a9f05e70
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825836"
---
# <a name="resetting-the-adapter-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーでのアダプターのリセット


## <span id="ddk_resetting_the_adapter_in_video_miniport_drivers_gg"></span><span id="DDK_RESETTING_THE_ADAPTER_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


コンピューターをハード再起動せずに、アダプターを初期化済み状態にリセットできない場合は、すべてのミニポートドライバーに[*HwVidResetHw*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_reset_hw)関数が必要です。

*HwVidResetHw*は、コンピューターがクラッシュしようとしている場合や、ユーザーがコンピューターのソフト再起動を開始した場合に、 *HAL*によって呼び出されます。 *HwVidResetHw*は、アダプターを指定された文字モードにリセットします。そのため、ソフト再起動中にシステムまたは初期化情報をシャットダウンするときに、HAL はクラッシュダンプ情報を表示できます。

*HwVidResetHw*は、BIOS を呼び出すことはできません。ページング可能なコードを呼び出すことも、ページング可能にすることもできません。 可能な場合は、**Videoportread * * * xxx*関数と **VideoPortWrite * * * xxx*関数だけを呼び出す必要がありますが、次のいずれかを呼び出すこともできます。

[**VideoPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstallexecution)

[**VideoPortZeroDeviceMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzerodevicememory)

[**Videoportゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportzeromemory)

 

 





