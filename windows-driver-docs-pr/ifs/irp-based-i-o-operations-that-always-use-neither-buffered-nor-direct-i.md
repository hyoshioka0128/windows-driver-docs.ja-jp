---
title: IRP に基づく I/O 操作を使用していないバッファー Nor ダイレクト I/O
description: IRP ベースの I/O 操作は常にバッファーもダイレクト I/O を使用します。
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- バッファーも直接 I/O WDK のファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc9d0d19c96d9de25160ba5ca5bbd67ab652086
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551978"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>IRP ベースの I/O 操作は常にバッファーもダイレクト I/O を使用します。


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


次の IRP ベースの I/O 操作は常にどちらもバッファーを使用しての値に関係なくダイレクト I/O、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)、ファイル システム ボリュームの構造。

-   IRP\_MJ\_PNP

-   IRP\_MJ\_クエリ\_セキュリティ

-   IRP\_MJ\_設定\_セキュリティ

-   IRP\_MJ\_システム\_コントロール

 

 




