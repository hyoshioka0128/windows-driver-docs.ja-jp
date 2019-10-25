---
title: DispatchFlushBuffers ルーチン
description: DispatchFlushBuffers ルーチン
ms.assetid: 091ce55c-e867-4ba4-aa25-5c20af45d9c2
keywords:
- ディスパッチルーチン WDK カーネル、DispatchFlushBuffers ルーチン
- DispatchFlushBuffers ルーチン
- IRP_MJ_FLUSH_BUFFERS i/o 関数のコード
- フラッシュバッファーディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5306fc37299eedbfa7799db1aec04d60f4f63479
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838730"
---
# <a name="dispatchflushbuffers-routines"></a>DispatchFlushBuffers ルーチン





ドライバーの[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers) I/o 関数コードの irp を処理します。 この i/o 関数コードに対するドライバーのサポートは省略可能ですが、内部データバッファーを保持するすべてのファイルシステムおよびフィルタードライバーは、ファイルデータまたはメタデータに対する変更をシステムシャットダウン間で保持するために処理する必要があります。 この要求は、バッファー内のデータをディスクにフラッシュする必要がある場合に、i/o マネージャーと他のオペレーティングシステムコンポーネント、およびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが[**Flushfilebuffers**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-flushfilebuffers)を呼び出すときに送信されます。

 

 




