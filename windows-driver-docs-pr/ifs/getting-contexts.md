---
title: コンテキストの取得
description: コンテキストの取得
ms.assetid: e0e659e5-6f95-4378-8764-63d96c7d07d4
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65b5d74ddda725c48621620076973e2550ea0277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841229"
---
# <a name="getting-contexts"></a>コンテキストの取得


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルタードライバーによってオブジェクトのコンテキストが設定されると、 **Fltget***xxx***コンテキスト**を呼び出すことによってコンテキストを取得できます。ここで、 *Xxx*はコンテキストの種類です。

次のコード例では、SwapBuffers サンプルミニフィルタードライバーを使用して、 [**Fltgetvolumecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)を呼び出してボリュームコンテキストを取得します。

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

[**Fltgetvolumecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)の呼び出しが成功した場合、*コンテキスト*パラメーターは呼び出し元のボリュームコンテキストのアドレスを受け取ります。 **Fltgetvolumecontext**は、*コンテキスト*ポインターの参照カウントをインクリメントします。 このため、このポインターが不要になった場合、ミニフィルタードライバーは[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出して解放する必要があります。

 

 




