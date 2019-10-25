---
title: ビデオミニポートドライバーの割り込み
description: ビデオミニポートドライバーの割り込み
ms.assetid: bf84a3fb-860a-4647-ac34-93f3a22b166b
keywords:
- ビデオミニポートドライバー WDK Windows 2000、割り込み
- WDK の割り込みビデオミニポート
- HwVidInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc50c73094b3c9ee6daa6cb0166bcdd996617792
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840354"
---
# <a name="interrupts-in-video-miniport-drivers"></a>ビデオミニポートドライバーの割り込み


## <span id="ddk_interrupts_in_video_miniport_drivers_gg"></span><span id="DDK_INTERRUPTS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


割り込みを生成するアダプターのビデオミニポートドライバーは、 [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)ルーチンを実装する必要があります。 ミニポートドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)ルーチンは、割り込みハンドラーを指すように、 [**VIDEO\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)構造の**HwInterrupt**メンバーを初期化する必要があります。

ビデオポートドライバーは、アダプターが割り込みを生成した場合にビデオミニポートドライバーの割り込みオブジェクトを設定します。 割り込みオブジェクトはビデオポートドライバーによって作成および管理されるため、ビデオミニポートドライバーライターは、割り込みオブジェクトについての詳細情報を必要としません。

ミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)関数が、ビデオアダプターが実際に割り込みを生成しないこと、またはアダプターの有効な割り込みベクター/レベルを判別できないことを検出した場合、 *HwVidFindAdapter*は両方**を設定する必要があります。InterruptLevel**および**InterruptVector** in THE [**VIDEO\_PORT\_CONFIG\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)構造体を0に設定します。

*HwVidFindAdapter*が制御を返すと、ビデオポートドライバーは、VIDEO\_PORT\_CONFIG\_INFO の割り込み構成メンバーを確認し、両方とも0の場合はミニポートドライバーの割り込みを接続しません。 *HwVidFindAdapter*で両方の割り込み構成メンバーを0に明示的に設定すると、ミニポートドライバーの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)関数によって設定された[*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)エントリポイントがある場合は無効になります。

*HwVidInterrupt*は、非ページ化されているため、ミニポートドライバーのデバイス拡張機能にアクセスできることに注意してください。 ミニポートドライバーの設計によっては、他のドライバー機能が*HwVidInterrupt*を使用してデバイス拡張機能またはデバイス拡張機能の特定の領域を安全に共有することが不可能な場合があります。

たとえば、ミニポートドライバーの[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数が、アダプターの割り込み時にデバイス拡張機能にアクセスしているとします。 *HwVidInterrupt*は別のプロセッサで実行され、 *HwVidInterrupt*はデバイス拡張機能にもアクセスします。 このような状況が発生する可能性がある場合、 *HwVidStartIO*は、ドライバーによって提供される[*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)関数を使用して[**VideoPortSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution)を呼び出す必要があります。

ビデオミニポートドライバーは、次の2つの規則に従う必要があります。

1.  ミニポートドライバーとハードウェアが D0 以外の状態になっている場合は、ハードウェアによって割り込みが生成される*ことはありません*。

2.  ルール1では、電源状態が D3 の場合、デバイスドライバ ISR は割り込みを処理し*ない*ようにする必要があります ( **FALSE**が返されます)。

 

 





