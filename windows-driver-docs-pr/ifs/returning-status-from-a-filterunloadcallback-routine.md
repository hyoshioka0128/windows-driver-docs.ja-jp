---
title: FilterUnloadCallback ルーチンから返される状態
description: FilterUnloadCallback ルーチンから返される状態
ms.assetid: 6fdaadc7-860d-49d6-833c-64624f435fd3
keywords:
- 状態値 WDK ファイルシステム
- ステータス WDK ファイルシステムを返す
- アンロード操作の拒否
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 396875f5222916d2f17123b7af0baa2166850079
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840990"
---
# <a name="returning-status-from-a-filterunloadcallback-routine"></a>FilterUnloadCallback ルーチンから返される状態


## <span id="ddk_returning_status_from_a_filterunloadcallback_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


ミニフィルタードライバーの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、通常、正常\_状態を返します。

必須ではないアンロード操作を拒否するには、ミニフィルタードライバーは、状態\_FLT などの適切な警告またはエラーの NTSTATUS 値を返す必要があります\_DO\_切断\_します。 必須のアンロード操作の詳細については、「 [FilterUnloadCallback ルーチンを記述する](writing-a-filterunloadcallback-routine.md)」および「 [**PFLT\_FILTER\_アンロード\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)」を参照してください。

*FilterUnloadCallback*ルーチンが警告またはエラーの NTSTATUS 値を返し、アンロード操作が必須ではない場合、ミニフィルタードライバーはアンロードされません。

 

 




