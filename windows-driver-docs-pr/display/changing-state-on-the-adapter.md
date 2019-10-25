---
title: アダプターの状態の変更
description: アダプターの状態の変更
ms.assetid: bf503a42-ac32-4d68-9ad9-afec69c5fe2a
keywords:
- ビデオアダプターの状態の変更 WDK ビデオミニポート
- 状態 WDK ビデオミニポート
- アダプターの状態 WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6daa8d74a0ebec3f72ebe3c4fdff6ea9aea3dd4a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839811"
---
# <a name="changing-state-on-the-adapter"></a>アダプターの状態の変更


## <span id="ddk_changing_state_on_the_adapter_gg"></span><span id="DDK_CHANGING_STATE_ON_THE_ADAPTER_GG"></span>


ミニポートドライバーは、 [*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)ルーチンが呼び出されるまで、アダプターの状態を完全に変更することはできません。 *HwVidInitialize*の前に呼び出されたミニポートドライバールーチン ( [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)など) では、ビデオアダプターの状態を不必要に変更しないでください。ビデオアダプターの状態を完全に変更することはできません。

[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)の実行中は、システムブートプロセスの初期段階で画面に情報を書き込むことができるように、HAL はビデオアダプターを制御します。 *HwVidFindAdapter*がアダプタを識別しようとしたときにアダプタの状態に影響を与える場合、このルーチンは元の状態を直ちに復元する必要があります。これにより、HAL は*HwVidFindAdapter*から戻るときに、起動メッセージを引き続き表示できます。

たとえば、 [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)は、アダプターの DAC 型を[*HwVidInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_initialize)関数に対して決定する必要があります。これは、ミニポートドライバーが読み込まれるかどうかには影響しませんが、アダプターが完全に。

 

 





