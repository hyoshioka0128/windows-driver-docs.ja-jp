---
title: ビデオ ミニポート ドライバーでのアダプターのリセット
description: ビデオ ミニポート ドライバーでのアダプターのリセット
ms.assetid: 321a5b6c-5a70-4acb-bf88-42ffb0cff86d
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、アダプターをリセットします。
- アダプターの WDK ビデオのミニポートをリセットします。
- HwVidResetHw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b2755ed8ce36af4420eda8408b97b811a1fdc0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385659"
---
# <a name="resetting-the-adapter-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーでのアダプターのリセット


## <span id="ddk_resetting_the_adapter_in_video_miniport_drivers_gg"></span><span id="DDK_RESETTING_THE_ADAPTER_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


すべてのミニポート ドライバーが必要、 [ *HwVidResetHw* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_reset_hw)関数の場合は、アダプターは、マシンのハード再起動せずに初期化された状態にリセットできません。

*HwVidResetHw*によって呼び出される、 *HAL*マシンがクラッシュしている場合、またはユーザーがコンピューターの再起動を開始する場合。 *HwVidResetHw* HAL がシャット ダウンする論理的な再起動中にシステムまたは初期化については、クラッシュ ダンプの情報を表示できるように、指定した文字モードにアダプターをリセットします。

*HwVidResetHw*呼び出すことはできません、ページング可能なコードを呼び出すことはできません、BIOS もが行われる可能性がページング可能な。 のみを呼び出す必要が可能な場合、**VideoPortRead * * * Xxx*と **VideoPortWrite * * * Xxx*が関数も呼び出すことができます、次のいずれか。

[**VideoPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstallexecution)

[**VideoPortZeroDeviceMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzerodevicememory)

[**VideoPortZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportzeromemory)

 

 





