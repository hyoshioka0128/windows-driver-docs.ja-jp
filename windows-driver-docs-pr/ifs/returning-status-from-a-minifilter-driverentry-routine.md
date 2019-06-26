---
title: ミニフィルター DriverEntry ルーチンから返される状態
description: ミニフィルター DriverEntry ルーチンから返される状態
ms.assetid: a9448908-f712-43f7-99c0-e02abc1678ed
keywords:
- 状態値 WDK ファイル システム
- WDK のファイル システムの状態を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 674dfc788bad0b87b53d289286b8d8482d5dac36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385941"
---
# <a name="returning-status-from-a-minifilter-driverentry-routine"></a>ミニフィルター DriverEntry ルーチンから返される状態


## <span id="ddk_returning_status_from_a_minifilter_driverentry_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_MINIFILTER_DRIVERENTRY_ROUTINE_IF"></span>


ミニフィルター ドライバーの**DriverEntry**ルーチンが通常の状態を返します\_成功します。 ミニフィルターの初期化に失敗した場合は、 **DriverEntry**ルーチンは、適切なエラー NTSTATUS 値を返す必要があります。

場合、 **DriverEntry**ミニフィルター ドライバーをアンロードして、ルーチンが成功 NTSTATUS 値ではない状態の値を返すシステムが応答します。 ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは呼び出されません。 このため、 **DriverEntry**ルーチンは、成功 NTSTATUS 値ではない状態の値を返す前にシステム リソースの割り当てられたメモリを解放する必要があります。

 

 




