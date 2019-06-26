---
title: ミニフィルター ドライバー用の FilterUnloadCallback ルーチンの記述
description: ミニフィルター ドライバー用の FilterUnloadCallback ルーチンの記述
ms.assetid: 0f4eac6d-08ef-47d5-8c1f-5397f058ecb2
keywords:
- ファイル システム ミニフィルター ドライバー WDK、FilterUnloadCallback ルーチン
- ミニフィルター ドライバー WDK、FilterUnloadCallback ルーチン
- FilterUnloadCallback
- ルーチン WDK ファイル システム ミニフィルターをアンロードします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3803c30268ba3fe240a32a23e183459db9ec1c95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356328"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>ミニフィルター ドライバー用の FilterUnloadCallback ルーチンの記述


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


ファイル システム ミニフィルター ドライバーに登録できます必要に応じて、 [ **PFLT\_フィルター\_アンロード\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)-としてミニフィルター ドライバーのルーチンを型指定された*FilterUnloadCallback*ルーチン。 このコールバック ルーチンはミニフィルター ドライバーのとして呼ば*ルーチンをアンロード*します。

ミニフィルター ドライバーは、登録する必要はありません、 *FilterUnloadCallback*ルーチン。 ただし、強くお勧めミニフィルター ドライバーがこのコールバック ルーチンを登録するため、ミニフィルター ドライバーが登録していない場合、 *FilterUnloadCallback* 、日常的なドライバーをアンロードできません。

ミニフィルター ドライバーが、PFLT のアドレスを格納するこのコールバック ルーチンを登録する\_フィルター\_アンロード\_のコールバックに型指定されたルーチン、 **FilterUnloadCallback** のメンバー[ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)ミニフィルター ドライバーは、パラメーターとして渡される構造[ **FltRegisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)でその**DriverEntry**ルーチン。

このセクションの内容:

[FilterUnloadCallback ルーチンが呼び出された場合](when-the-filterunloadcallback-routine-is-called.md)

[FilterUnloadCallback ルーチンを記述します。](writing-a-filterunloadcallback-routine.md)

 

 




