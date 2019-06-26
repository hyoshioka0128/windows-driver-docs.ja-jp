---
title: DispatchShutdown ルーチン
description: DispatchShutdown ルーチン
ms.assetid: e0d4ed56-a614-4dc8-9bb2-abfe38f05946
keywords:
- IRP_MJ_SHUTDOWN I/O 関数のコード
- ディスパッチ ルーチンの WDK カーネル、DispatchShutdown ルーチン
- DispatchShutdown ルーチン
- シャット ダウン ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f93fd8a4c832dd88ead14d9ffdd82d44e0556f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384967"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown ルーチン





ドライバーの[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_シャット ダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown) I/O関数のコードです。 データの内部キャッシュがある大容量記憶装置のドライバーでは、この要求を処理する必要があります。 大容量記憶装置のドライバーと上層にあるそれらの中間ドライバーを基になるドライバーには、データの内部バッファーが保持している場合この要求処理する必要がありますもします。

 

 




