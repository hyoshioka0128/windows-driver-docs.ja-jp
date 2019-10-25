---
title: コンテキストの設定
description: コンテキストの設定
ms.assetid: 3daa23e6-14d7-4d35-8bc8-695296cd289d
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、設定
- コンテキストのアタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca82bc563401c820a3851c2df20ffce86c86f7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840964"
---
# <a name="setting-contexts"></a>コンテキストの設定


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


新しいコンテキストを作成した後、ミニフィルタードライバーは**FltSet***xxx***コンテキスト**を呼び出すことによってオブジェクトにアタッチできます。ここで、 *xxx*はコンテキストの種類です。

**FltSet***xxx***コンテキスト**ルーチンの*Operation*パラメーターが FLT に設定されている場合\_\_コンテキスト\_設定し、\_が存在する場合は\_を保持します。また、 **FltSet***xxx***コンテキスト**は、新しく割り当てられたコンテキストをにアタッチします。ミニフィルタードライバーがオブジェクトのコンテキストをまだ設定していない場合にのみオブジェクト。 ミニフィルタードライバーによってコンテキストが既に設定されている場合、 **FltSet***Xxx***コンテキスト**は、既に\_定義されている状態\_FLT\_\_を返します。これは、既に NTSTATUS エラーコードであり、既存のコンテキストに置き換わるものではありません。 **FltSet***Xxx***コンテキスト**ルーチンの*oldcontext*パラメーターが**NULL**以外の場合は、既存のコンテキストへのポインターを受け取ります。 このポインターが不要になった場合、ミニフィルタードライバーは[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)を呼び出すことにより、このポインターを解放する必要があります。

*Operation*パラメーターが FLT に設定されている場合\_\_コンテキスト\_\_設定します。\_が存在する場合、 **FltSet***Xxx***コンテキスト**は常に新しいコンテキストをオブジェクトにアタッチします。 ミニフィルタードライバーによってコンテキストが既に設定されている場合、 **FltSet***Xxx***コンテキスト**によって既存のコンテキストが削除され、新しいコンテキストが設定され、新しいコンテキストの参照カウントがインクリメントされます。 *Oldcontext*パラメーターが**NULL**以外の場合は、削除されたコンテキストへのポインターを受け取ります。 このポインターが不要になった場合、ミニフィルタードライバーは**FltReleaseContext**を呼び出すことにより、このポインターを解放する必要があります。

次のコード例では、CTX サンプルミニフィルタードライバーを**使用して**、インスタンスコンテキストを作成し、設定します。

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

[**Fltsetinstancecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)を呼び出した後は、 **FltReleaseContext**を呼び出して、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)によって設定された参照カウント ( **fltsetinstancecontext**では*ない*) を解放することに注意してください。 これについては、「[コンテキストの解放](releasing-contexts.md)」で説明しています。

 

 




