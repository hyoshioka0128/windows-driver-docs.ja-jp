---
title: デバイス オブジェクト フラグに従う IRP ベースの I/O 操作
description: デバイス オブジェクト フラグに従う IRP ベースの I/O 操作
ms.assetid: d322aeda-a753-4616-8a35-1a5ae5a37cf2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 306c6863154b589055f95f7489e790b52c1bed6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379481"
---
# <a name="irp-based-io-operations-that-obey-device-object-flags"></a>デバイス オブジェクト フラグに従う IRP ベースの I/O 操作


## <span id="ddk_irp_based_io_operations_that_obey_device_object_flags_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_OBEY_DEVICE_OBJECT_FLAGS_IF"></span>


次の IRP ベースの I/O 操作のバッファリング メソッドは、の値によって決まりますが、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体ファイル システム ボリューム。

-   IRP\_MJ\_ディレクトリ\_コントロール

-   IRP\_MJ\_クエリ\_EA

-   IRP\_MJ\_クエリ\_クォータ

-   IRP\_MJ\_READ

-   IRP\_MJ\_設定\_EA

-   IRP\_MJ\_SET\_QUOTA

-   IRP\_MJ\_WRITE

DO\_バッファーに格納された\_IO、および操作を行います\_直接\_IO でフラグを設定、**フラグ**メンバーが次のように使用します。

-   場合、操作を行います\_バッファーに格納された\_IO フラグが設定されて、操作がバッファー内の I/O を使用します。

-   場合、操作を行います\_直接\_IO フラグが設定され、DO\_バッファーに格納された\_IO フラグが設定されていない、操作がダイレクト I/O を使用します。

-   どちらのフラグが設定されている場合、操作には、バッファーも直接 I/O が使用されます。

デバイス オブジェクトのフラグの詳細については、次を参照してください。 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)と[デバイス オブジェクトを初期化して](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)します。

注その IRP\_MJ\_読み取りおよび IRP\_MJ\_書き込みは IRP ベースまたは高速の I/O 操作を指定できます。 IRP ベースできたら、バッファリングのメソッドは上記で説明したようにデバイス オブジェクトのフラグによって決まります。 これらの操作が高速の I/O の場合、バッファーのどちらを使用して、常にもダイレクト I/O。 IRP ベースまたは高速の I/O 操作は、I/O 操作の詳細については、次を参照してください。[操作することができますが IRP ベースまたは高速の I/O](operations-that-can-be-irp-based-or-fast-i-o.md)します。

 

 




