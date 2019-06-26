---
title: パフォーマンスは、HwStartIo 中に完了する要求をヒントします。
description: パフォーマンスは、HwStartIo 中に完了する要求をヒントします。
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 476354ba5f39792cab08f072a54a2d779b25272c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358475"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>パフォーマンスのヒント: HwStartIo 中の要求の完了


完了の準備ができている未処理の I/O 要求を完了してその[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチン、ミニポートは IRQL (DIRQL)、システムの応答性を向上するには、デバイスで時間を費やすことができ、システムの応答性と I/O スループットをさらに向上させる新しい Storport 最適化も活用します。 ポイントは、割り込みハンドラーで可能なほとんどの時間をかけずにしようとします。 活用するために、次のように新しい Storport 最適化ミニポート。

-   使用して DPC リダイレクトを有効にする必要があります[ **StorPortInitializePerfOpts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitializeperfopts)

-   使用する必要があります[ **StorPortNotification (NotificationType = RequestComplete)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)でその[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチンに通知するには完了した I/O 要求の Storport

-   完了-StartIo 中に、ストレージの設定を行うには意図を示す必要があります\_PERF\_最適化\_の\_完了\_に\_呼び出しでSTARTIOフラグ[ **StorPortInitializePerfOpts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitializeperfopts)ルーチン

-   最適化が適用される前に存在する必要のある (たとえば、要求のサイズとスループット) のワークロードの特性を決定する必要があります。

内でその[ **HwStorStartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチン、ミニポートを確認する完了した要求、要求された I/O 操作の開始後にします。

 

 




