---
title: ミニフィルタードライバー用の FilterUnloadCallback ルーチンの作成
description: ミニフィルタードライバー用の FilterUnloadCallback ルーチンの作成
ms.assetid: 0f4eac6d-08ef-47d5-8c1f-5397f058ecb2
keywords:
- ファイルシステムミニフィルタードライバー WDK、FilterUnloadCallback ルーチン
- ミニフィルタードライバー WDK、FilterUnloadCallback ルーチン
- FilterUnloadCallback
- アンロードルーチン WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 119110e6c9489f95a4cc91ad59bbc2be0de19366
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840926"
---
# <a name="writing-a-filterunloadcallback-routine-for-a-minifilter-driver"></a>ミニフィルタードライバー用の FilterUnloadCallback ルーチンの作成


## <span id="ddk_writing_a_filterunloadcallback_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


ファイルシステムミニフィルタードライバーでは、必要に応じて、 [**PFLT\_FILTER\_\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)型のルーチンをミニフィルタードライバーの*FilterUnloadCallback*ルーチンとしてアンロードできます。 このコールバックルーチンは、ミニフィルタードライバーの*アンロードルーチン*とも呼ばれます。

ミニフィルタードライバーは、 *FilterUnloadCallback*ルーチンを登録するためには必要ありません。 ただし、ミニフィルタードライバーでは、 *FilterUnloadCallback*ルーチンが登録されていない場合、ドライバーをアンロードできないため、このコールバックルーチンを登録することを強くお勧めします。

このコールバックルーチンを登録するために、ミニフィルタードライバーは、PFLT\_FILTER のアドレス\_アンロード\_コールバック型のルーチンを、 [**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体の**FilterUnloadCallback**メンバーに格納します。ミニパスドライバーは、 **Driverentry**ルーチンの[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡します。

このセクションの内容は次のとおりです。

[FilterUnloadCallback ルーチンが呼び出されたとき](when-the-filterunloadcallback-routine-is-called.md)

[FilterUnloadCallback ルーチンを記述する](writing-a-filterunloadcallback-routine.md)

 

 




