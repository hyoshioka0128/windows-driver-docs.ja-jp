---
title: 同期されていない IdeHwBuildIo ルーチン
description: 同期されていない IdeHwBuildIo ルーチン
ms.assetid: 47e32f05-5c89-4423-b515-c774b94a9b84
keywords:
- ATA ポートドライバー WDK、同期
- 同期 WDK ATA ポートドライバー
- AtaHwBuildIo
- 非同期処理の WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca1b2e1fd2655df29e71db877edf9c8dac5546ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844439"
---
# <a name="unsynchronized-idehwbuildio-routine"></a>同期されていない IdeHwBuildIo ルーチン


## <span id="ddk_unsynchronized_atahwbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_ATAHWBUILDIO_ROUTINE_KG"></span>


**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。


Ata ポートドライバーは、ATA ミニポートドライバーの開始 i/o ルーチン[**IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio)を呼び出す前に\_レベル以上をディスパッチするプロセッサの IRQL を発生させます。 ATA ポートドライバーは、割り込みをマスクアウトし、開始 i/o ルーチンと割り込みハンドラーが重要なオペレーティングシステム構造へのアクセスを同期することを保証するために、プロセッサの IRQL を発生させます。 ポートの開始時にミニポートドライバーが開始 i/o ルーチンで使用する時間を短縮するには、&gt;= ディスパッチ\_レベルで、 [**IdeHwBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio)ルーチンを提供します。 ATA ポートドライバーは、IRQL &lt;= ディスパッチ\_レベルで*IdeHwBuildIo*を呼び出します。これにより、ミニポートドライバーは、低 irql でできるだけ多くの i/o 要求を前処理し、プロセッサの制御を独占するのを回避できます。

Storport i/o モデルでは、同様の手法を使用して、開始 i/o ルーチンで費やされる時間を最小限に抑えています。 Storport ドライバーで[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)を使用する方法の詳細については、「同期されていない[HwStorBuildIo ルーチン](unsynchronized-hwstorbuildio-routine.md)」を参照してください。

デバイス拡張機能などの重要なシステム構造へのアクセスを必要とする i/o 要求のすべての処理は、 [**IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio)ルーチン内で実行する必要があります。

 

 


