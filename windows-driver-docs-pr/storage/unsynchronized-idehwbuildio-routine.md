---
title: 同期されていない IdeHwBuildIo ルーチン
description: 同期されていない IdeHwBuildIo ルーチン
ms.assetid: 47e32f05-5c89-4423-b515-c774b94a9b84
keywords:
- ATA ポート ドライバー WDK、同期
- WDK ATA ポート ドライバーの同期
- AtaHwBuildIo
- 同期されていない処理 WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6d45776c89414e257d399e801664a603e958a21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581691"
---
# <a name="unsynchronized-idehwbuildio-routine"></a>同期されていない IdeHwBuildIo ルーチン


## <span id="ddk_unsynchronized_atahwbuildio_routine_kg"></span><span id="DDK_UNSYNCHRONIZED_ATAHWBUILDIO_ROUTINE_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA ポート ドライバーは、ディスパッチするプロセッサの IRQL を発生させます。\_レベルまたはの上を呼び出す前に、ATA ミニポート ドライバーの起動 I/O ルーチン、 [ **IdeHwStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff559003)します。 ATA ポート ドライバーは、割り込みをマスクして開始の I/O ルーチンと、割り込みハンドラーが重要なオペレーティング システムの構造体へのアクセスを同期することを保証するために、プロセッサの IRQL を発生させます。 ミニポート ドライバーは、IRQL で開始 I/O ルーチンに費やされた時間を短縮する&gt;= ディスパッチ\_レベルに、ミニポート ドライバーには、 [ **IdeHwBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557462)ルーチン。 ATA のポート ドライバー呼び出し*IdeHwBuildIo* IRQL で&lt;= ディスパッチ\_レベル、ミニポート ドライバーを低い IRQL でできるだけ多くの I/O 要求の前処理し、コントロールを独占しないようにするため、プロセッサ。

Storport の I/O モデルでは、その開始 I/O ルーチンに費やした時間を最小限に同様の手法を使用します。 Storport ドライバーの使用方法の詳細については[ **HwStorBuildIo**](https://msdn.microsoft.com/library/windows/hardware/ff557369)を参照してください、[同期されていない HwStorBuildIo ルーチン](unsynchronized-hwstorbuildio-routine.md)します。

内で、デバイスの拡張機能などの重要なシステムの構造体へのアクセスを必要とする I/O 要求のすべての処理を行う必要があります、 [ **IdeHwStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff559003)ルーチン。

 

 


