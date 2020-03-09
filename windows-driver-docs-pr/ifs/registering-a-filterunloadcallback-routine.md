---
title: FilterUnloadCallback ルーチンの登録
description: FilterUnloadCallback ルーチンの登録
ms.assetid: 0f4eac6d-08ef-47d5-8c1f-5397f058ecb2
keywords:
- ファイルシステムミニフィルタードライバー WDK、FilterUnloadCallback ルーチン
- ミニフィルタードライバー WDK、FilterUnloadCallback ルーチン
- FilterUnloadCallback
- アンロードルーチン WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc31dab494d4e380772ceb6e087836de243c4790
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910535"
---
# <a name="registering-a-filterunloadcallback-routine"></a>FilterUnloadCallback ルーチンの登録

ファイルシステムミニフィルタードライバーでは、必要に応じて[**PFLT_FILTER_UNLOAD_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)型のルーチンをミニフィルタードライバーの*FilterUnloadCallback*ルーチンとして登録することもできます。 このコールバックルーチンは、ミニフィルタードライバーの*アンロードルーチン*とも呼ばれます。

ミニフィルタードライバーは、 *FilterUnloadCallback*ルーチンを登録するためには必要ありません。 ただし、ミニフィルタードライバーでは、 *FilterUnloadCallback*ルーチンが登録されていない場合、ドライバーをアンロードできないため、このコールバックルーチンを登録することを強くお勧めします。

このコールバックルーチンを登録するために、ミニパスドライバーは、PFLT_FILTER_UNLOAD_CALLBACK で型指定されたルーチンのアドレスを、 [**FLT_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体の**FilterUnloadCallback**メンバーに格納します。このメンバーは、ミニフィルタードライバーが、その**Driverentry**ルーチンの[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡します。
