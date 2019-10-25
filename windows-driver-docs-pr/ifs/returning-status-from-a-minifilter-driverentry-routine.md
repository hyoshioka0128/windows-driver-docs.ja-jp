---
title: ミニフィルター DriverEntry ルーチンから返される状態
description: ミニフィルター DriverEntry ルーチンから返される状態
ms.assetid: a9448908-f712-43f7-99c0-e02abc1678ed
keywords:
- 状態値 WDK ファイルシステム
- ステータス WDK ファイルシステムを返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c5c493934e2c764be319276f8cbf44638e21b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840989"
---
# <a name="returning-status-from-a-minifilter-driverentry-routine"></a>ミニフィルター DriverEntry ルーチンから返される状態


## <span id="ddk_returning_status_from_a_minifilter_driverentry_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_MINIFILTER_DRIVERENTRY_ROUTINE_IF"></span>


ミニフィルタードライバーの**Driverentry**ルーチンは、正常に完了した状態\_返します。 ただし、ミニフィルターの初期化が失敗した場合は、 **Driverentry**ルーチンから適切なエラー NTSTATUS 値が返されます。

**Driverentry**ルーチンが、成功した NTSTATUS 値ではない状態値を返した場合、システムはミニフィルタードライバーをアンロードすることによって応答します。 ミニフィルタードライバーの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは呼び出されません。 このため、 **Driverentry**ルーチンは、システムリソースに割り当てられたメモリを解放してから、成功した NTSTATUS 値ではない状態値を返す必要があります。

 

 




