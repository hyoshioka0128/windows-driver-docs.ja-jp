---
title: デバイス オブジェクト フラグに従う IRP ベースの I/O 操作
description: デバイス オブジェクト フラグに従う IRP ベースの I/O 操作
ms.assetid: d322aeda-a753-4616-8a35-1a5ae5a37cf2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dbcb1db232aed838e4f08dccf691140f3e65379
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841184"
---
# <a name="irp-based-io-operations-that-obey-device-object-flags"></a>デバイス オブジェクト フラグに従う IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_obey_device_object_flags_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_OBEY_DEVICE_OBJECT_FLAGS_IF"></span>


次の IRP ベース i/o 操作のバッファリングメソッドは、ファイルシステムボリュームの[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーの値によって決まります。

-   IRP\_MJ\_DIRECTORY\_コントロール

-   IRP\_MJ\_クエリ\_EA

-   IRP\_MJ\_クエリ\_クォータ

-   IRP\_MJ\_READ

-   IRP\_MJ\_設定\_EA

-   IRP\_MJ\_設定\_クォータ

-   IRP\_MJ\_WRITE

DO\_バッファー\_IO と、 **flags**メンバー内のダイレクト\_io フラグを\_するために、次のように使用されます。

-   DO\_バッファリング\_IO フラグが設定されている場合、操作はバッファー i/o を使用します。

-   DO\_DIRECT\_IO フラグが設定されていて、DO\_バッファリング\_IO フラグが設定されていない場合、操作は直接 i/o を使用します。

-   どちらのフラグも設定されていない場合、操作ではバッファーも直接 i/o も使用されません。

デバイスオブジェクトフラグの詳細については、「[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)」と「[デバイスオブジェクトの初期化](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)」を参照してください。

IRP\_MJ\_READ および IRP\_\_MJ の書き込みは、IRP ベースまたは高速の i/o 操作であることに注意してください。 IRP ベースの場合、バッファリングメソッドは、前述のデバイスオブジェクトフラグによって決定されます。 これらの操作が高速 i/o の場合は、バッファーも直接も使用されません。 IRP ベースまたは高速 i/o 操作の i/o 操作の詳細については、「 [irp ベースまたは高速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o を使用できる操作」を参照してください。

 

 




