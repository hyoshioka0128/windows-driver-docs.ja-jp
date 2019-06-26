---
title: バッファー処理された I/O を常に使用する IRP ベースの I/O 操作
description: バッファー処理された I/O を常に使用する IRP ベースの I/O 操作
ms.assetid: ac9b62a2-a562-4f40-83af-e1c74d58ce2b
keywords:
- バッファー内の I/O の WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e02664283d22df920f152b950300071b8296e079
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360873"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>バッファー処理された I/O を常に使用する IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


次の IRP ベースの I/O 操作は常の値に関係なく、バッファー内の I/O を使用して、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)用の構造ファイル システム ボリューム:

-   IRP\_MJ\_作成 ([**EaBuffer パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create))

-   IRP\_MJ\_QUERY\_INFORMATION

-   IRP\_MJ\_クエリ\_ボリューム\_情報

-   IRP\_MJ\_SET\_INFORMATION

-   IRP\_MJ\_設定\_ボリューム\_情報

注その IRP\_MJ\_クエリ\_情報は、高速の I/O 操作にもできます。 高速な I/O 操作であるバッファーも直接 I/O が使用されます。 IRP ベースまたは高速の I/O 操作は、I/O 操作の詳細については、次を参照してください。[操作することができますが IRP ベースまたは高速の I/O](operations-that-can-be-irp-based-or-fast-i-o.md)します。

 

 




