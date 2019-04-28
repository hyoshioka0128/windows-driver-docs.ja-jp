---
title: コンテキストの取得
description: コンテキストの取得
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- ファイル システム ミニフィルターの WDK のコンテキストを取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b9c17b94974189899b796ec8aac72249b646f00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370333"
---
# <a name="getting-contexts"></a>コンテキストの取得


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


呼び出すことで、コンテキストを取得できるミニフィルター ドライバーがオブジェクトのコンテキストを設定すると、 **FltGet***Xxx***コンテキスト**ここで、 *Xxx*コンテキスト型です。

ミニフィルター ドライバーを呼び出し、SwapBuffers サンプル ミニフィルター ドライバーから取得した次のコード例で[ **FltGetVolumeContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543189)ボリューム コンテキストを取得します。

```cpp
status = FltGetVolumeContext(
 FltObjects->Filter,    //Filter
 FltObjects->Volume,    //Volume
                &volCtx);              //Context
...
if (volCtx != NULL) {
 FltReleaseContext(volCtx);
}
```

場合への呼び出し[ **FltGetVolumeContext** ](https://msdn.microsoft.com/library/windows/hardware/ff543189)は成功しますが、*コンテキスト*パラメーターは、呼び出し元のボリュームのコンテキストのアドレスを受け取ります。 **FltGetVolumeContext** 、参照カウントをインクリメント、*コンテキスト*ポインター。 したがって、このポインターは必要がなくなったら、ミニフィルター ドライバーする必要がありますリリース呼び出して[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)します。

 

 




