---
title: DispatchShutdown ルーチン
description: DispatchShutdown ルーチン
ms.assetid: e0d4ed56-a614-4dc8-9bb2-abfe38f05946
keywords:
- IRP_MJ_SHUTDOWN i/o 関数のコード
- ディスパッチルーチン WDK カーネル、DispatchShutdown ルーチン
- DispatchShutdown ルーチン
- シャットダウンディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae881fdf0204d9bbc30410765be72b616b4df4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836826"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown ルーチン





ドライバーの[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_シャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)I/o 関数コードの irp を処理します。 データの内部キャッシュがある大容量記憶装置のドライバーは、この要求を処理する必要があります。 基になるドライバーがデータの内部バッファーを保持している場合は、大容量記憶装置と中間ドライバーのドライバーもこの要求を処理する必要があります。

 

 




