---
title: FilterUnloadCallback ルーチンから状態を返す
description: FilterUnloadCallback ルーチンから状態を返す
ms.assetid: 6fdaadc7-860d-49d6-833c-64624f435fd3
keywords:
- 状態値 WDK ファイル システム
- WDK のファイル システムの状態を返す
- アンロード操作を拒否しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28366e44f850590ff82b71ab6227bdd68def06f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557107"
---
# <a name="returning-status-from-a-filterunloadcallback-routine"></a>FilterUnloadCallback ルーチンから状態を返す


## <span id="ddk_returning_status_from_a_filterunloadcallback_routine_if"></span><span id="DDK_RETURNING_STATUS_FROM_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


ミニフィルター ドライバーの[ **FilterUnloadCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンが通常の状態を返します\_成功します。

ミニフィルター ドライバーは必須ではないアンロード操作を拒否する状態など適切な警告またはエラー NTSTATUS 値を返す必要があります\_FLT\_は\_いない\_デタッチします。 必須のアンロード操作の詳細については、次を参照してください[FilterUnloadCallback ルーチンを記述](writing-a-filterunloadcallback-routine.md)と[ **PFLT\_フィルター\_アンロード\_コールバック。**](https://msdn.microsoft.com/library/windows/hardware/ff551085).

場合、 *FilterUnloadCallback*ルーチンが警告またはエラー NTSTATUS 値を返すと、アンロード操作はありませんが、ミニフィルター ドライバーはアンロードされません。

 

 




