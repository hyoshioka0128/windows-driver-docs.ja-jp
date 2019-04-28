---
title: C28152
description: 警告 C28152 AddDevice などの関数からの戻り値が予期せず DO_DEVICE_INITIALIZING します。
ms.assetid: df2b68dc-b22b-4aaa-b1ba-b34bfdd9b886
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28152
ms.openlocfilehash: e848f95770f8d2d2358e72931a4fad11d9a3eb8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361353"
---
# <a name="c28152"></a>C28152


C28152 を警告します。AddDevice などの関数からの戻り値が予期せずに行う\_デバイス\_初期化しています

ドライバーが返さその**AddDevice**ルーチン、または同様のユーティリティ ルーチンが、**は\_デバイス\_初期化**のビット、**フラグ**word (**デバイス オブジェクト -&gt;フラグ**) で、**デバイス オブジェクト**ルーチンは消去されません。

**AddDevice**ルーチンをクリアするには、次のようなコードを含める必要があります、**は\_デバイス\_初期化**フラグ。

```
FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
```

詳細については**AddDevice**ルーチンを参照してください[関数またはフィルター ドライバーで AddDevice ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff540529)

 

 





