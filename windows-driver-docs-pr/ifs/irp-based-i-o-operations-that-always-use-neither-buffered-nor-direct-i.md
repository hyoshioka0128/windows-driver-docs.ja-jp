---
title: IRP に基づく I/O 操作を使用していないバッファー Nor ダイレクト I/O
description: バッファー処理された I/O またはダイレクト I/O を常に使用しない IRP ベースの I/O 操作
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- バッファーも直接 I/O WDK のファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc9d0d19c96d9de25160ba5ca5bbd67ab652086
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379715"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>バッファー処理された I/O またはダイレクト I/O を常に使用しない IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


次の IRP ベースの I/O 操作は常にどちらもバッファーを使用しての値に関係なくダイレクト I/O、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)、ファイル システム ボリュームの構造。

-   IRP\_MJ\_PNP

-   IRP\_MJ\_クエリ\_セキュリティ

-   IRP\_MJ\_設定\_セキュリティ

-   IRP\_MJ\_SYSTEM\_CONTROL

 

 




