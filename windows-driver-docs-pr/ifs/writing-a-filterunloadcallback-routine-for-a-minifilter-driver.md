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
ms.openlocfilehash: f8593d83f89624b486201acbd2b0a2e8bac93483
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322192"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>ミニフィルター ドライバー用の FilterUnloadCallback ルーチンの記述


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


ファイル システム ミニフィルター ドライバーに登録できます必要に応じて、 [ **PFLT\_フィルター\_アンロード\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551085)-としてミニフィルター ドライバーのルーチンを型指定された*FilterUnloadCallback*ルーチン。 このコールバック ルーチンはミニフィルター ドライバーのとして呼ば*ルーチンをアンロード*します。

ミニフィルター ドライバーは、登録する必要はありません、 *FilterUnloadCallback*ルーチン。 ただし、強くお勧めミニフィルター ドライバーがこのコールバック ルーチンを登録するため、ミニフィルター ドライバーが登録していない場合、 *FilterUnloadCallback* 、日常的なドライバーをアンロードできません。

ミニフィルター ドライバーが、PFLT のアドレスを格納するこのコールバック ルーチンを登録する\_フィルター\_アンロード\_のコールバックに型指定されたルーチン、 **FilterUnloadCallback** のメンバー[ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)ミニフィルター ドライバーは、パラメーターとして渡される構造[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)でその**DriverEntry**ルーチン。

このセクションの内容:

[FilterUnloadCallback ルーチンが呼び出された場合](when-the-filterunloadcallback-routine-is-called.md)

[FilterUnloadCallback ルーチンを記述します。](writing-a-filterunloadcallback-routine.md)

 

 




