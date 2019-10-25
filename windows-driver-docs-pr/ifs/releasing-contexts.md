---
title: コンテキストのリリース
description: コンテキストのリリース
ms.assetid: 29d855cd-cca6-486b-86d9-f74810ae12c1
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、リリース
- コンテキストの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c7d15b90923d4c29723c2fcca0febb914726dc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841000"
---
# <a name="releasing-contexts"></a>コンテキストのリリース


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルタードライバーは、 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出すことによってコンテキストを解放します。 次のいずれかのルーチンの呼び出しが成功するたびに、 **FltReleaseContext**の呼び出しによって最終的に一致する必要があります。

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetFileContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetfilecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetTransactionContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgettransactioncontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)

**FltSet***Xxx***コンテキスト**によって返される*Oldcontext*ポインターと[**Fltdeletecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)によって返される*コンテキスト*ポインターも、不要になったときに解放する必要があることに注意してください。

次のコード例では、CTX サンプルミニフィルタードライバーを**使用して**、インスタンスコンテキストを作成および設定してから、 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出します。

```cpp
status = FltAllocateContext(
           FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
           NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
...
status = FltSetInstanceContext(
           FltObjects->Instance,              //Instance
           FLT_SET_CONTEXT_KEEP_IF_EXISTS,    //Operation
           instanceContext,                   //NewContext
           NULL);                             //OldContext

if (instanceContext != NULL) {
  FltReleaseContext(instanceContext);
}
return status;
```

[**Fltsetinstancecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)の呼び出しが成功したかどうかに関係なく、 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)が呼び出されることに注意してください。 どちらの場合も、呼び出し元は**FltReleaseContext**を呼び出して、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)によって参照セットを解放する必要があります ( **fltsetinstancecontext**ではありません)。

インスタンスに対してコンテキストが正常に設定されている場合は、 [**Fltsetinstancecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)によってインスタンスコンテキストに独自の参照が追加されます。 したがって、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)によって設定された参照は不要になり、 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出すと削除されます。

[**Fltsetinstancecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)の呼び出しが失敗した場合、インスタンスコンテキストには参照が1つだけあります。つまり、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)によって設定されています。 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)がを返した場合、インスタンスコンテキストの参照カウントはゼロであり、フィルターマネージャーによって解放されます。

 

 




