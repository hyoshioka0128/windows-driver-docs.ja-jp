---
title: コンテキストの作成
description: コンテキストの作成
ms.assetid: da62d79d-064b-4ea4-abed-ffb13a9cc13d
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041b4c827da92c5d3673b88ef0ff10917cb1d16d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841448"
---
# <a name="creating-contexts"></a>コンテキストの作成


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


ミニフィルタードライバーが使用するコンテキストの種類を登録すると、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)を呼び出すことによってコンテキストを作成できます。 このルーチンは、「[コンテキスト型の登録](registering-context-types.md)」で説明されている条件に従って、使用する適切なコンテキスト定義を選択します。

次のコード例では、CTX サンプルミニフィルタードライバーから取得した、 **Ctxinstancesetup**ルーチンは[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)を呼び出してインスタンスコンテキストを作成します。

```cpp
status = FltAllocateContext(
 FltObjects->Filter,           //Filter
           FLT_INSTANCE_CONTEXT,         //ContextType
           CTX_INSTANCE_CONTEXT_SIZE,    //ContextSize
 NonPagedPool,                 //PoolType
           &instanceContext);            //ReturnedContext
```

CTX サンプルでは、インスタンスコンテキストに対して次のコンテキスト定義が登録されています。

```cpp
{ FLT_INSTANCE_CONTEXT,              //ContextType
  0,                                 //Flags
 CtxContextCleanup,                 //ContextCleanupCallback
  CTX_INSTANCE_CONTEXT_SIZE,         //Size
  CTX_INSTANCE_CONTEXT_TAG },        //PoolTag
```

**サイズ**メンバーが定数であるため、これは固定サイズのコンテキスト定義です。 (**サイズ**のメンバーが\_変数\_サイズ\_コンテキストの場合は、変数サイズのコンテキスト定義になります)。FLTFL\_コンテキスト\_登録\_\_正確な\_サイズ\_一致フラグが**フラグ**メンバーで設定されていないことに注意してください。 この場合、 [**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)の*size*パラメーターの値がコンテキスト定義の**size**メンバーの値と一致すると、 **FltAllocateContext**は適切な非ページルックからインスタンスコンテキストを割り当てます。表. 値が一致しない場合、 **FltAllocateContext**は STATUS\_FLT\_コンテキスト\_割り当て\_見つかりませ\_んでした。

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)は、新しいコンテキストの参照カウントを1に初期化します。 コンテキストが不要になった場合は、ミニフィルタードライバーがこの参照を解放する必要があります。 そのため、 **FltAllocateContext**のすべての呼び出しは、 [**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)の後続の呼び出しで一致する必要があります。

 

 




