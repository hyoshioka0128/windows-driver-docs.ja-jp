---
title: FilterUnloadCallback ルーチンの記述
description: FilterUnloadCallback ルーチンの記述
ms.assetid: 2f680770-38af-4dcb-93b8-7f770e0378b2
keywords:
- FilterUnloadCallback
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26f9b8ad3b08012defb2d12c27ffa95af7d744f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322225"
---
# <a name="writing-a-filterunloadcallback-routine"></a>FilterUnloadCallback ルーチンの記述


## <span id="ddk_writing_a_filterunloadcallback_routine_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


*FilterUnloadCallback*ルーチンは次のように定義されます。

```cpp
typedef NTSTATUS
(*PFLT_FILTER_UNLOAD_CALLBACK) (
    FLT_FILTER_UNLOAD_FLAGS Flags
    );
```

*FilterUnloadCallback*ルーチンが 1 つの入力パラメーター*フラグ*、される**NULL**または FLTFL\_フィルター\_アンロード\_必須。 フィルター マネージャーでは、このパラメーターを設定する FLTFL\_フィルター\_アンロード\_必須アンロード操作が必須であることを示します。 このパラメーターの詳細については、次を参照してください。 [ **PFLT\_フィルター\_アンロード\_コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551085)します。

ミニフィルター ドライバーの*FilterUnloadCallback*ルーチンは、次の手順を実行する必要があります。

-   開いているカーネル モードの通信サーバー ポートで処理をすべて閉じます。

-   呼び出す[ **FltUnregisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544606)ミニフィルター ドライバーの登録を解除します。

-   必要なグローバル クリーンアップを実行します。

-   適切な NTSTATUS 値を返します。

このセクションの内容:

[通信サーバー ポートを閉じる](closing-the-communication-server-port.md)

[ミニフィルターの登録を解除](unregistering-the-minifilter.md)

[グローバルのクリーンアップを実行します。](performing-global-cleanup.md)

[FilterUnloadCallback ルーチンから状態を返す](returning-status-from-a-filterunloadcallback-routine.md)

 

 




