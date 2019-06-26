---
title: コンテキストの取得
description: コンテキストの取得
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- ファイル システム ミニフィルターの WDK のコンテキストを取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f644c53e895b7283e1cc72c8ec66a06b9e0c4ea6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365898"
---
# <a name="getting-contexts"></a>コンテキストの取得


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


呼び出すことで、コンテキストを取得できるミニフィルター ドライバーがオブジェクトのコンテキストを設定すると、 **FltGet***Xxx***コンテキスト**ここで、 *Xxx*コンテキスト型です。

ミニフィルター ドライバーを呼び出し、SwapBuffers サンプル ミニフィルター ドライバーから取得した次のコード例で[ **FltGetVolumeContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)ボリューム コンテキストを取得します。

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

場合への呼び出し[ **FltGetVolumeContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)は成功しますが、*コンテキスト*パラメーターは、呼び出し元のボリュームのコンテキストのアドレスを受け取ります。 **FltGetVolumeContext** 、参照カウントをインクリメント、*コンテキスト*ポインター。 したがって、このポインターは必要がなくなったら、ミニフィルター ドライバーする必要がありますリリース呼び出して[ **FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)します。

 

 




