---
title: ミニフィルター ドライバーでの I/O 操作のフィルタリング
description: ミニフィルター ドライバーでの I/O 操作のフィルタリング
ms.assetid: e35944c1-fcc6-44e0-838c-da8d24f95d51
keywords:
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、ガイドライン
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、ガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad47dcef5e8dd67c4e4aad26e6bf99bfc2d87ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841397"
---
# <a name="filtering-io-operations-in-a-minifilter-driver"></a>ミニフィルター ドライバーでの I/O 操作のフィルタリング


## <span id="ddk_filtering_io_operations_in_a_minifilter_driver_if"></span><span id="DDK_FILTERING_IO_OPERATIONS_IN_A_MINIFILTER_DRIVER_IF"></span>


次の一覧では、ファイルシステムミニフィルタードライバーで特定の種類の i/o 操作をフィルター処理するためのガイドラインについて説明します。

-   IRP\_MJ\_CREATE の[**preoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)は、ファイル、ストリーム、またはストリームハンドルのコンテキストを照会または設定できません。これは、作成されるファイルまたはストリーム (存在する場合) がまだ決定されていないためです。

-   IRP\_MJ\_CLOSE の[**postoperation コールバックルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)は、ファイル、ストリーム、またはストリームハンドルのコンテキストを設定または照会できません。これらの項目に関連付けられているシステム内部構造体は、ポストクローズの前に解放されるためです。ルーチンが呼び出されます。

-   ミニフィルタードライバーは、IRP\_MJ\_CLEANUP または IRP\_MJ\_CLOSE 操作に失敗しないようにする必要があります。 これらの操作は、保留にするか、フィルターマネージャーに返すことができます。または、STATUS\_SUCCESS で完了します。 ただし、preoperation コールバックルーチンは、これらの操作を失敗させないようにする必要があります。

-   ミニフィルタードライバーは、IRP\_MJ\_シャットダウンの postoperation コールバックルーチンを登録できません。

 

 




