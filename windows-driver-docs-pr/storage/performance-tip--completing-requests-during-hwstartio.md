---
title: HwStartIo 中のパフォーマンスに関するヒントの完了要求
description: HwStartIo 中のパフォーマンスに関するヒントの完了要求
ms.assetid: b1a3feff-ca18-4757-a336-c70ada998ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2306eb8a287161add12ab2578b8fdeff45258f6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842728"
---
# <a name="performance-tip-completing-requests-during-hwstartio"></a>パフォーマンスのヒント: HwStartIo 中の要求の完了


[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)ルーチンでの完了の準備ができている未処理の i/o 要求を完了することで、ミニポートはデバイスの IRQL (dirql) で時間を短縮できます。これにより、システムの応答性が向上します。また、新しい Storport 最適化も利用できます。システムの応答性と i/o スループットをさらに向上させます。 この時点では、割り込みハンドラーでできるだけ少ない時間を使用しようとします。 新しい Storport の最適化を利用するには、ミニポートを使用します。

-   [ **Storportinitializeperfopts**よる DPC リダイレクトを有効にする必要があります](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts)

-   完了した i/o 要求を Storport に通知するには、 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)ルーチンで[**Storportnotification (NotificationType = requestcomplete)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)を使用する必要があります

-   StartIo の実行中は、 [**Storportinitializeperfopts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializeperfopts)ルーチンの呼び出しの\_STARTIO フラグ中に\_\_、\_の完了\_の\_を最適化することによって、完了時に完了することを示す必要があります。

-   最適化を適用する前に存在する必要があるワークロードの特性 (要求サイズやスループットなど) を決定する必要があります。

[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)ルーチンでは、要求された i/o 操作の開始後に、ミニポートは完了した要求を確認する必要があります。

 

 




