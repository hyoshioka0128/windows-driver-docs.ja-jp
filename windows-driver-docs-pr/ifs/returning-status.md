---
title: 返される状態
description: 返される状態
ms.assetid: fd490517-f4c5-4e20-9eac-6a9ac7d04992
keywords:
- 状態値 WDK ファイル システム
- 成功状態の値の WDK ファイル システム
- WDK のファイル システムの状態を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42dfacd2daedcf2011e06d9eb3f90fa08ab6d36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344534"
---
# <a name="returning-status"></a>返される状態


## <span id="ddk_returning_status_if"></span><span id="DDK_RETURNING_STATUS_IF"></span>


ファイル システム フィルター ドライバーの**DriverEntry**ルーチンが通常の状態を返します\_成功します。 ただし、ドライバーの初期化に失敗した場合、 **DriverEntry**ルーチンは、該当するエラー状態の値を返す必要があります。

場合、 **DriverEntry**ルーチンが成功状態の値ではない状態の値を返す、システムのドライバーをアンロードして応答します。 このため、 **DriverEntry**常に、ルーチンは成功の状態の値ではない状態の値を返す前に、デバイス オブジェクトなどのシステム リソースの割り当てられたメモリを解放する可能性があります。

 

 




