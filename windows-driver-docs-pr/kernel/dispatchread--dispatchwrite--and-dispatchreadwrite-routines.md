---
title: DispatchRead、DispatchWrite、および DispatchReadWrite ルーチン
description: DispatchRead、DispatchWrite、および DispatchReadWrite ルーチン
ms.assetid: 2982939a-4afb-4b21-9a96-0ac758f0fb6c
keywords:
- DispatchRead ルーチン
- DispatchWrite ルーチン
- DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchRead ルーチン
- 読み取り/書き込みディスパッチルーチン WDK カーネル
- IRP_MJ_WRITE i/o 関数コード
- IRP_MJ_READ i/o 関数コード
- データ転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- データの転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd34f3de9a4926fb24fce991dcfaefc879616728
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838725"
---
# <a name="dispatchread-dispatchwrite-and-dispatchreadwrite-routines"></a>DispatchRead、DispatchWrite、および DispatchReadWrite ルーチン





ドライバーの[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)と[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)の i/o 関数コードを持つ irp を処理します。 また、結合された[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、これらの i/o 関数コードの両方に対して irp を処理できます。

データをシステムに転送できるデバイスのすべてのドライバーには、 *DispatchRead*ルーチンが必要です。 システムからデータを転送できるデバイスのすべてのドライバーには、 *DispatchWrite*ルーチンが必要です。 双方向にデータを転送するドライバーには、 *DispatchReadWrite*ルーチンを組み合わせることができます。

下位レベルのドライバーは、 **irp\_MJ\_READ**および**irp\_MJ\_書き込み**要求を非同期的に処理します。 したがって、最上位レベルのドライバーの*DispatchRead*ルーチンや*DispatchWrite*ルーチンは、要求に有効なパラメーターがあり、そのドライバーの I/O スタック位置が IRP である場合に、これらの要求をに渡す必要があります。

ドライバーがバッファーオブジェクトまたは直接 i/o 用にデバイスオブジェクトを設定するかどうかは、転送要求の処理方法に影響します。 特に、DMA 操作を行うための直接 i/o を使用するドライバーでは、 **irp\_MJ\_READ**または**irp\_MJ\_WRITE を満たすために、大規模な転送要求を一連の小さな転送操作に分割する必要がある場合があります。** 要求。 詳細については、「[入出力の手法](i-o-programming-techniques.md)」を参照してください。

次のサブセクションでは、バッファー i/o およびダイレクト i/o を使用する下位レベルのデバイスドライバーの*DispatchReadWrite*ルーチンの設計と実装に関するいくつかの考慮事項について説明します。また、上位レベルのドライバーについても説明します。

[転送の非同期処理](handling-transfers-asynchronously.md)

[バッファーされる i/o を使用した DispatchReadWrite](dispatchreadwrite-using-buffered-i-o.md)

[直接 i/o を使用した DispatchReadWrite](dispatchreadwrite-using-direct-i-o.md)

[上位レベルのドライバーでの DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)

[読み取り/書き込みディスパッチルーチンの概要](summary-of-read-write-dispatch-routines.md)

 

 




