---
title: パフォーマンスは、HwStartIo 中に完了する要求をヒントします。
description: パフォーマンスは、HwStartIo 中に完了する要求をヒントします。
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10e01b53f3c8d6d58326823989d63721e7bdf579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389394"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>パフォーマンスのヒント: HwStartIo 中の要求の完了


完了の準備ができている未処理の I/O 要求を完了してその[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423)ルーチン、ミニポートは IRQL (DIRQL)、システムの応答性を向上するには、デバイスで時間を費やすことができ、システムの応答性と I/O スループットをさらに向上させる新しい Storport 最適化も活用します。 ポイントは、割り込みハンドラーで可能なほとんどの時間をかけずにしようとします。 活用するために、次のように新しい Storport 最適化ミニポート。

-   使用して DPC リダイレクトを有効にする必要があります[ **StorPortInitializePerfOpts**](https://msdn.microsoft.com/library/windows/hardware/ff567114)

-   使用する必要があります[ **StorPortNotification (NotificationType = RequestComplete)** ](https://msdn.microsoft.com/library/windows/hardware/ff567446)でその[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423)ルーチンに通知するには完了した I/O 要求の Storport

-   完了-StartIo 中に、ストレージの設定を行うには意図を示す必要があります\_PERF\_最適化\_の\_完了\_に\_呼び出しでSTARTIOフラグ[ **StorPortInitializePerfOpts** ](https://msdn.microsoft.com/library/windows/hardware/ff567114)ルーチン

-   最適化が適用される前に存在する必要のある (たとえば、要求のサイズとスループット) のワークロードの特性を決定する必要があります。

内でその[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423)ルーチン、ミニポートを確認する完了した要求、要求された I/O 操作の開始後にします。

 

 




