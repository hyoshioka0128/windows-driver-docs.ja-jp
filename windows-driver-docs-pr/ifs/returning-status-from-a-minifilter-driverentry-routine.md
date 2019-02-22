---
title: ミニフィルター DriverEntry ルーチンから状態を返す
description: ミニフィルター DriverEntry ルーチンから状態を返す
ms.assetid: a9448908-f712-43f7-99c0-e02abc1678ed
keywords:
- 状態値 WDK ファイル システム
- WDK のファイル システムの状態を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9f7d305d3599b7d105f9580bd0812d7efd1ec95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528579"
---
# <a name="returning-status-from-a-minifilter-driverentry-routine"></a>ミニフィルター DriverEntry ルーチンから状態を返す


## <span id="ddk_returning_status_from_a_minifilter_driverentry_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_MINIFILTER_DRIVERENTRY_ROUTINE_IF"></span>


ミニフィルター ドライバーの**DriverEntry**ルーチンが通常の状態を返します\_成功します。 ミニフィルターの初期化に失敗した場合は、 **DriverEntry**ルーチンは、適切なエラー NTSTATUS 値を返す必要があります。

場合、 **DriverEntry**ミニフィルター ドライバーをアンロードして、ルーチンが成功 NTSTATUS 値ではない状態の値を返すシステムが応答します。 ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンは呼び出されません。 このため、 **DriverEntry**ルーチンは、成功 NTSTATUS 値ではない状態の値を返す前にシステム リソースの割り当てられたメモリを解放する必要があります。

 

 




