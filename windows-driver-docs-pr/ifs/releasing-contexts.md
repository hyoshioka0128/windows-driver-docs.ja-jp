---
title: コンテキストのリリース
description: コンテキストのリリース
ms.assetid: 29d855cd-cca6-486b-86d9-f74810ae12c1
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを解放します。
- コンテキストを解放します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffebd5d0640b18b2170802c0219665ed7cf282ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385123"
---
# <a name="releasing-contexts"></a>コンテキストのリリース


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーは、呼び出すことによって、コンテキストを解放[ **FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)します。 呼び出して、次のルーチンのいずれかにすべての成功した呼び出しを一致する必要が最終的に**FltReleaseContext**:

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetFileContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetfilecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetTransactionContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgettransactioncontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreferencecontext)

なお、 *OldContext*によって返されたポインター **FltSet***Xxx***コンテキスト**と*コンテキスト*によって返されたポインター [**FltDeleteContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)不要になったときにもリリースする必要があります。

次のコード例で、CTX サンプル ミニフィルター ドライバーから取得した、 **CtxInstanceSetup**ルーチンを作成するインスタンス コンテキストを設定および呼び出して[ **FltReleaseContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext):

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

なお[ **FltReleaseContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)呼びますかどうかに関係なくへの呼び出し[ **FltSetInstanceContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinstancecontext)が成功するとします。 どちらの場合も、呼び出し元が呼び出す必要があります**FltReleaseContext**によって設定の参照を解放する[ **FltAllocateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext) (いない**FltSetInstanceContext**).

コンテキストが正常にインスタンスの場合は設定されている場合[ **FltSetInstanceContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinstancecontext)インスタンス コンテキストに独自の参照を追加します。 参照を設定するために、 [ **FltAllocateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext)必要がなくなったらへの呼び出し[ **FltReleaseContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)削除されます。

場合に呼び出し[ **FltSetInstanceContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinstancecontext)が失敗したインスタンス コンテキストが 1 つだけ参照、つまりによって設定[ **FltAllocateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext). ときに[ **FltReleaseContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)インスタンス コンテキストが参照カウントは 0 とフィルター マネージャーが解放を返します。

 

 




