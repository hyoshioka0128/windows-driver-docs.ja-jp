---
title: FilterUnloadCallback ルーチンを記述する
description: FilterUnloadCallback ルーチンを記述する
ms.assetid: 2f680770-38af-4dcb-93b8-7f770e0378b2
keywords:
- FilterUnloadCallback
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feb776ebdf29cf7ab3443d346cf0627f8863670e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840924"
---
# <a name="writing-a-filterunloadcallback-routine"></a>FilterUnloadCallback ルーチンを記述する


## <span id="ddk_writing_a_filterunloadcallback_routine_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


*FilterUnloadCallback*ルーチンは次のように定義されています。

```cpp
typedef NTSTATUS
(*PFLT_FILTER_UNLOAD_CALLBACK) (
    FLT_FILTER_UNLOAD_FLAGS Flags
    );
```

*FilterUnloadCallback*ルーチンには1つの入力パラメーターがあります。 *Flags*は**NULL**または FLTFL\_フィルター\_アンロード\_必須です。 フィルターマネージャーは、アンロード操作が必須であることを示すために、このパラメーターを FLTFL\_FILTER\_UNLOAD\_必須に設定します。 このパラメーターの詳細については、「 [**PFLT\_FILTER\_UNLOAD\_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)」を参照してください。

ミニフィルタードライバーの*FilterUnloadCallback*ルーチンでは、次の手順を実行する必要があります。

-   開いているカーネルモード通信サーバーのポートハンドルを閉じます。

-   [**Fltunregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出してミニフィルタードライバーの登録を解除します。

-   必要なグローバルクリーンアップを実行します。

-   適切な NTSTATUS 値を返します。

このセクションの内容は次のとおりです。

[通信サーバーのポートを閉じています](closing-the-communication-server-port.md)

[ミニフィルターの登録解除](unregistering-the-minifilter.md)

[グローバルクリーンアップを実行しています](performing-global-cleanup.md)

[FilterUnloadCallback ルーチンから状態を返す](returning-status-from-a-filterunloadcallback-routine.md)

 

 




