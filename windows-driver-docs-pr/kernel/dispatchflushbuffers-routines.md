---
title: DispatchFlushBuffers ルーチン
description: DispatchFlushBuffers ルーチン
ms.assetid: 091ce55c-e867-4ba4-aa25-5c20af45d9c2
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchFlushBuffers ルーチン
- DispatchFlushBuffers ルーチン
- IRP_MJ_FLUSH_BUFFERS I/O 関数のコード
- フラッシュ バッファー ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3845c8ac75d5e59e62e076cf7da6798470bae5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384989"
---
# <a name="dispatchflushbuffers-routines"></a>DispatchFlushBuffers ルーチン





ドライバーの[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers) I/O 関数のコード。 この I/O 関数のコードのドライバー サポートは省略可能では、ファイル システムとフィルター ドライバーすべて内部のデータ バッファーを維持するには、システムがシャット ダウンの間でファイル データまたはメタデータへの変更を保持するように処理する必要があります。 この要求を送信 I/O マネージャーとその他のオペレーティング システムのコンポーネントに加えてその他のカーネル モード ドライバーでは、バッファー内のデータをフラッシュする必要がある場合をディスクにします。 たとえば、ユーザー モード アプリケーションを呼び出すときに送信される[ **FlushFileBuffers**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-flushfilebuffers)します。

 

 




