---
title: コンテキストのリリース
description: コンテキストのリリース
ms.assetid: 29d855cd-cca6-486b-86d9-f74810ae12c1
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを解放します。
- コンテキストを解放します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd7f28a6421bfbd784f0b276cbee9a1578be7408
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370114"
---
# <a name="releasing-contexts"></a>コンテキストのリリース


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルター ドライバーは、呼び出すことによって、コンテキストを解放[ **FltReleaseContext**](https://msdn.microsoft.com/library/windows/hardware/ff544314)します。 呼び出して、次のルーチンのいずれかにすべての成功した呼び出しを一致する必要が最終的に**FltReleaseContext**:

[**FltAllocateContext**](https://msdn.microsoft.com/library/windows/hardware/ff541710)

[**FltGetInstanceContext**](https://msdn.microsoft.com/library/windows/hardware/ff543058)

[**FltGetFileContext**](https://msdn.microsoft.com/library/windows/hardware/ff543025)

[**FltGetStreamContext**](https://msdn.microsoft.com/library/windows/hardware/ff543144)

[**FltGetStreamHandleContext**](https://msdn.microsoft.com/library/windows/hardware/ff543155)

[**FltGetTransactionContext**](https://msdn.microsoft.com/library/windows/hardware/ff543175)

[**FltGetVolumeContext**](https://msdn.microsoft.com/library/windows/hardware/ff543189)

[**FltReferenceContext**](https://msdn.microsoft.com/library/windows/hardware/ff544291)

なお、 *OldContext*によって返されたポインター **FltSet***Xxx***コンテキスト**と*コンテキスト*によって返されたポインター [**FltDeleteContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541960)不要になったときにもリリースする必要があります。

次のコード例で、CTX サンプル ミニフィルター ドライバーから取得した、 **CtxInstanceSetup**ルーチンを作成するインスタンス コンテキストを設定および呼び出して[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314):

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

なお[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)呼びますかどうかに関係なくへの呼び出し[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)が成功するとします。 どちらの場合も、呼び出し元が呼び出す必要があります**FltReleaseContext**によって設定の参照を解放する[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710) (いない**FltSetInstanceContext**).

コンテキストが正常にインスタンスの場合は設定されている場合[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)インスタンス コンテキストに独自の参照を追加します。 参照を設定するために、 [ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710)必要がなくなったらへの呼び出し[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)削除されます。

場合に呼び出し[ **FltSetInstanceContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544521)が失敗したインスタンス コンテキストが 1 つだけ参照、つまりによって設定[ **FltAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff541710). ときに[ **FltReleaseContext** ](https://msdn.microsoft.com/library/windows/hardware/ff544314)インスタンス コンテキストが参照カウントは 0 とフィルター マネージャーが解放を返します。

 

 




