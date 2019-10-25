---
title: ミニフィルターの登録解除
description: ミニフィルターの登録解除
ms.assetid: 4af2d4fd-bfbe-4a75-bbfb-2a1c4b5c2032
keywords:
- ミニフィルターの登録解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a1dd0527c5a5589660371e7c9991bee62548922
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840945"
---
# <a name="unregistering-the-minifilter"></a>ミニフィルターの登録解除


## <span id="ddk_unregistering_the_minifilter_if"></span><span id="DDK_UNREGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルタードライバーの[**FilterUnloadCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、ミニフィルタードライバーの登録を解除するために[**Fltunregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出す必要があります。 **Fltunregisterfilter**を呼び出すと、次の処理が行われます。

-   ミニフィルタードライバーのコールバックルーチンが登録解除されます。

-   ミニフィルタードライバーのインスタンスが破棄され、ミニフィルタードライバーの[**InstanceTeardownStartCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)ルーチンと**InstanceTeardownCompleteCallback**ルーチンが各ミニフィルタードライバーインスタンスに対して呼び出されます。

-   ミニフィルタードライバーによって、ボリューム、インスタンス、ストリーム、またはストリームハンドルにコンテキストが設定されている場合、これらのコンテキストは削除されます。 ミニフィルタードライバーによって特定のコンテキスト型に対して[**cleanupcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)コールバックルーチンが登録されている場合、フィルターマネージャーはコンテキストを削除する前に*cleanupcontext*ルーチンを呼び出します。

ミニフィルタドライバーの不透明なフィルターポインターに未処理のランダウン参照がある場合、 **Fltunregisterfilter**は削除されるまで待機状態になります。 未処理ランダウン参照は、通常、ミニフィルタードライバーが[**Fltqueuegenericworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)を呼び出して、作業項目をシステム作業キューに挿入し、作業項目がまだデキューされて処理されていないことが原因で発生します。 (フィルターマネージャーは、ミニフィルタードライバーが**Fltqueuegenericworkitem**を呼び出したときにランダウン参照を追加し、ミニフィルタードライバーの作業ルーチンから制御が戻ったときに、この参照を削除します)。

また、 [**Fltobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltobjectreference)や[**FltGetFilterFromInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilterfrominstance)などの、ミニフィルタードライバーの非透過フィルターポインターにランダウン参照を追加するルーチンをミニフィルタードライバーが呼び出した場合にも、未処理のランダウン参照が発生する可能性があります。後で[**Fltobjectdereference 参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltobjectdereference)を呼び出すことはありません。

 

 




