---
title: バッファーも直接 i/o も使用しない IRP ベース i/o 操作
description: バッファー処理された I/O またはダイレクト I/O を常に使用しない IRP ベースの I/O 操作
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- バッファーも直接 i/o WDK ファイルシステムもありません
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307caef3d68bf6bdb15769e66152582e70f26367
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841186"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>バッファー処理された I/O またはダイレクト I/O を常に使用しない IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


次の IRP ベースの i/o 操作では、ファイルシステムボリュームの[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーの値に関係なく、バッファーも直接 i/o も使用されません。

-   IRP\_MJ\_PNP

-   IRP\_MJ\_クエリ\_セキュリティ

-   IRP\_MJ\_設定\_セキュリティ

-   IRP\_MJ\_SYSTEM\_CONTROL

 

 




