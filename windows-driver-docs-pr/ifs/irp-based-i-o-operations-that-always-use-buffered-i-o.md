---
title: バッファー処理された I/O を常に使用する IRP ベースの I/O 操作
description: バッファー処理された I/O を常に使用する IRP ベースの I/O 操作
ms.assetid: ac9b62a2-a562-4f40-83af-e1c74d58ce2b
keywords:
- バッファーされた i/o WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e96c871b96c2008d08447d5a9f7f45f15887d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841189"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>バッファー処理された I/O を常に使用する IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


次の IRP ベースの i/o 操作では、ファイルシステムボリュームのオブジェクト構造の**フラグ**メンバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の値に関係なく、常にバッファー内 i/o を使用します。

-   IRP\_MJ\_CREATE ([**EaBuffer parameter**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create))

-   IRP\_MJ\_QUERY\_INFORMATION

-   IRP\_MJ\_クエリ\_ボリューム\_情報

-   IRP\_MJ\_SET\_INFORMATION

-   IRP\_MJ\_\_ボリューム\_情報の設定

IRP\_MJ\_クエリ\_情報も、高速 i/o 操作であることに注意してください。 高速な i/o 操作では、バッファーも直接 i/o も使用されません。 IRP ベースまたは高速 i/o 操作の i/o 操作の詳細については、「 [irp ベースまたは高速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o を使用できる操作」を参照してください。

 

 




