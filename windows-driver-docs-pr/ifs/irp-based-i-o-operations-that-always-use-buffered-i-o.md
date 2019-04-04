---
title: バッファー内の I/O を使用して、常に IRP ベースの I/O 操作
description: バッファー内の I/O を使用して、常に IRP ベースの I/O 操作
ms.assetid: ac9b62a2-a562-4f40-83af-e1c74d58ce2b
keywords:
- バッファー内の I/O の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3608b75196aa9ee62191193edaa8a0d524a0db2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549825"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>バッファー内の I/O を使用して、常に IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


次の IRP ベースの I/O 操作は常の値に関係なく、バッファー内の I/O を使用して、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)用の構造ファイル システム ボリューム:

-   IRP\_MJ\_作成 ([**EaBuffer パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff544687))

-   IRP\_MJ\_クエリ\_情報

-   IRP\_MJ\_クエリ\_ボリューム\_情報

-   IRP\_MJ\_設定\_情報

-   IRP\_MJ\_設定\_ボリューム\_情報

注その IRP\_MJ\_クエリ\_情報は、高速の I/O 操作にもできます。 高速な I/O 操作であるバッファーも直接 I/O が使用されます。 IRP ベースまたは高速の I/O 操作は、I/O 操作の詳細については、[操作することができますが IRP ベースまたは高速の I/O](operations-that-can-be-irp-based-or-fast-i-o.md)を参照してください。

 

 




