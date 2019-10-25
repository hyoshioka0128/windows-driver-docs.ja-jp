---
title: HwVidSynchronizeExecutionCallback ルーチンの実装
description: HwVidSynchronizeExecutionCallback ルーチンを実装する場合
ms.assetid: d33736ca-aff2-421b-a8cc-d09eba76ff7f
keywords:
- ビデオミニポートドライバー WDK Windows 2000、割り込み
- WDK の割り込みビデオミニポート
- HwVidSynchronizeExecutionCallback
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 5c6608285b1c4ad8903efe95c5cc6756e8b3dc36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829148"
---
# <a name="implementing-a-hwvidsynchronizeexecutioncallback-routine"></a>HwVidSynchronizeExecutionCallback ルーチンの実装

割り込みを生成しないアダプターのミニポートドライバーは、 [*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)関数を使用して[**VideoPortSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution)を呼び出すことはめったにありません。

実際、 [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)関数を持つミニポートドライバーでも、必ずしも*HwVidSynchronizeExecutionCallback*関数を持つことはできません。 ビデオポートドライバーは、前の要求の処理が完了するまでミニポートドライバーの[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数に要求を送信しないため (詳細については、「[ビデオ要求の処理 (Windows 2000 モデル)](processing-video-requests--windows-2000-model-.md) 」を参照)、ミニポートドライバーが**VideoPortSynchronizeExecution**を呼び出すことはほとんどありません。

ミニポートドライバーの*HwVidSynchronizeExecutionCallback*関数には、次の2つの用途が考えられます。

-   アダプターレジスタにアクセスするには、 *HwVidInterrupt*関数以外のドライバー関数のミニポートドライバーのデバイス拡張機能を使用します。

    *HwVidSynchronizeExecutionCallback*関数が制御されている場合、アダプターからの割り込みはマスクされないので、ミニポートドライバーの*HwVidInterrupt*関数は、*デバイス拡張機能の状態を変更できません。HwVidSynchronizeExecutionCallback*関数は SMP マシンで実行されています。

-   アダプターが必要とする場合に、アダプターの登録またはポートへのコマンドの書き込みが非常に高速になります。

    *HwVidSynchronizeExecutionCallback*関数に制御が与えられている場合、ほとんどのシステム割り込みはマスクされないため、 *HwVidSynchronizeExecutionCallback*関数はデバイス (またはクロック) の割り込みによって割り込まれることはありません。

    *HwVidSynchronizeExecutionCallback*関数は、できるだけ早く制御を返す*必要があり*ます。

最初の種類の[*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)関数を使用すると、ミニポートドライバーは[**VideoPortSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution)を呼び出し、*優先順位*を**VpMediumPriority**に設定します。 2番目の種類*の HwVidSynchronizeExecutionCallback*関数では、ドライバーに[*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)関数がない場合、ミニポートドライバーによって、*優先順位*が**VpMediumPriority**に設定されたこの呼び出しも行われます。 それ以外の場合、このようなミニポートドライバーは、*優先順位*を**VpHighPriority**に設定してこの呼び出しを行います。

一般に、ミニポートドライバーでは、 *HwVidSynchronizeExecutionCallback*関数の2番目の型を使用して**VideoPortSynchronizeExecution**を呼び出す*ことはできません*。ただし、ドライバーデザイナーに他の代替手段がない場合は、アダプターがである場合を除きます。そのため、システム割り込みがマスクされないようにプログラミングする必要があります。 それ以外の場合、ミニポートドライバーは、*優先順位*が**VVideoPortSynchronizeExecution wpriority**に設定されたを呼び出す必要があります。

*HwVidSynchronizeExecutionCallback*関数は、 *HwVidInterrupt*関数のように、ページングすることはできません。また、システムを停止することなく、特定の **VideoPort * * * Xxx*関数を呼び出すことはできません。 *HwVidSynchronizeExecutionCallback*関数が安全に呼び出すことができる **VideoPort * * * Xxx*関数の概要については、 [*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)を参照してください。

 

 





