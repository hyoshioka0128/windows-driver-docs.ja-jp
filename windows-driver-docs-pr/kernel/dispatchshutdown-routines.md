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
ms.openlocfilehash: ba42a3be1d4e7c9d8005e75f0843dbe4c4227d65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535418"
---
# <a name="dispatchshutdown-routines"></a>DispatchShutdown ルーチン





ドライバーの[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンの Irp の処理、 [ **IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff550807) I/O関数のコードです。 データの内部キャッシュがある大容量記憶装置のドライバーでは、この要求を処理する必要があります。 大容量記憶装置のドライバーと上層にあるそれらの中間ドライバーを基になるドライバーには、データの内部バッファーが保持している場合この要求処理する必要がありますもします。

 

 




