---
title: HwVidSynchronizeExecutionCallback ルーチンの実装
description: いつ HwVidSynchronizeExecutionCallback ルーチンを実装するには
ms.assetid: d33736ca-aff2-421b-a8cc-d09eba76ff7f
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、割り込み
- WDK のビデオのミニポートを中断します。
- HwVidSynchronizeExecutionCallback
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 9199dc35ebe2e7f46f145848ba307f791dacb5b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386242"
---
# <a name="implementing-a-hwvidsynchronizeexecutioncallback-routine"></a>HwVidSynchronizeExecutionCallback ルーチンの実装

ほとんどの割り込みを生成しないアダプターのミニポート ドライバーを呼び出す[ **VideoPortSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportsynchronizeexecution)で、 [ *HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_synchronize_routine)関数。

実際には、ミニポート ドライバーがあっても、 [ *HwVidInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)関数の必要はありません、 *HwVidSynchronizeExecutionCallback*関数。 ビデオ ポート ドライバーでは、ミニポート ドライバーの要求が送信されないため、 [ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)直前の要求の処理が完了するまで機能 (を参照してください[ビデオの処理要求 (Windows 2000 モデル)](processing-video-requests--windows-2000-model-.md)詳細については)、ミニポート ドライバーを呼び出すことはほとんどありません**VideoPortSynchronizeExecution**します。

ミニポート ドライバーの 2 つの用途がある*HwVidSynchronizeExecutionCallback*関数。

-   アダプターにアクセスする登録以外の関数のドライバー、ミニポート ドライバーのデバイスの拡張機能を使用して、 *HwVidInterrupt*関数。

    ときに、 *HwVidSynchronizeExecutionCallback*アダプターからの割り込みをマスク関数がコントロールを与えられると、これをオフ、ミニポート ドライバーの*HwVidInterrupt*関数での状態を変更することはできません、中にデバイスの拡張機能、 *HwVidSynchronizeExecutionCallback*関数は、SMP マシンで実行されています。

-   コマンドを非常に高速アダプター レジスタまたはポートを記述して、アダプター、必要なかどうか。

    ときに、 *HwVidSynchronizeExecutionCallback*関数に制御が与えられる、off、ほぼすべてのシステムの割り込みがマスクされるため、 *HwVidSynchronizeExecutionCallback*関数は、によって割り込まれることはできません、デバイス (またはクロックにも、) を中断します。

    *HwVidSynchronizeExecutionCallback*関数*する必要があります*可能な限り早く制御を戻します。

最初の型と[ *HwVidSynchronizeExecutionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_synchronize_routine)関数では、ミニポート ドライバー呼び出し[ **VideoPortSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportsynchronizeexecution)で、*優先度*設定**VpMediumPriority**します。 2 番目の型と*HwVidSynchronizeExecutionCallback*関数、ミニポート ドライバーも、この呼び出しで、*優先度*に設定**VpMediumPriority**場合、ドライバーがにない[ *HwVidInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)関数。 それ以外の場合、この呼び出しでは、このようなミニポート ドライバー、*優先度*設定**VpHighPriority**します。

一般に、ミニポート ドライバーが必要があります*いない*呼び出す**VideoPortSynchronizeExecution**の 2 番目の型と*HwVidSynchronizeExecutionCallback*しない限り、機能、ドライバー デザイナーには、他の代替手段はありません。 つまり、アダプターはのようにプログラミングする必要がありますようにしない限り、システムの割り込みマスク オフに指定します。 ミニポート ドライバーを呼び出す必要がありますそれ以外の場合、 **VideoPortSynchronizeExecution**で、*優先度*に設定**VpLowPriority**します。

A *HwVidSynchronizeExecutionCallback*関数は、このような*HwVidInterrupt*関数、ページングすることはできませんを呼び出せません特定 **ビデオ ポート * * * Xxx*関数。システムを持ち出さずにします。 概要については **ビデオ ポート * * * Xxx*関数を*HwVidSynchronizeExecutionCallback*関数は、安全に呼び出すことができますを参照してください[ *HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt).

 

 





