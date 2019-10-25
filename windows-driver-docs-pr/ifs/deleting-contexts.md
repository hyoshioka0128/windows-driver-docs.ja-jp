---
title: コンテキストの削除
description: コンテキストの削除
ms.assetid: 43a30a75-4344-4fc5-ad57-28b48c2e54a8
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、削除
- コンテキストの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b2a6fef077e7525cfa7164bf20989dc9038b399
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841440"
---
# <a name="deleting-contexts"></a>コンテキストの削除


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


**FltSet***Xxx***コンテキスト**への正常な呼び出しによって設定されたすべてのコンテキストは、最終的には削除される必要があります。 ただし、フィルターマネージャーは、アタッチされたオブジェクトが削除されたとき、ミニフィルタードライバーインスタンスがボリュームからデタッチされたとき、またはミニフィルタードライバーがアンロードされたときに、コンテキストを自動的に削除します。 そのため、ミニフィルタードライバーでコンテキストを明示的に削除する必要はほとんどありません。

ミニフィルタードライバーでは、 **Fltdelete***xxx***コンテキスト**を呼び出すことによってコンテキストを削除できます。ここで、 *xxx*はコンテキストの種類であり、 [**fltdeletecontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)を呼び出します。

コンテキストは、オブジェクトに対して現在設定されている場合にのみ削除できます。 コンテキストは、まだ設定されていない場合、または**FltSet***Xxx***コンテキスト**への正常な呼び出しによって既に置き換えられている場合は、削除できません。

**Fltdelete***Xxx***コンテキスト**への呼び出しでは、古いコンテキストが**NULL**以外の場合は、 *oldcontext*パラメーターで返されます。 *Oldcontext*パラメーターが**NULL**の場合、フィルターマネージャーはコンテキストの参照カウントをデクリメントします。これは、ミニフィルタードライバーが未処理の参照を持っていない限り解放されます。

次のコード例は、ストリームコンテキストを削除する方法を示しています。

```cpp
status = FltDeleteStreamContext(
 FltObjects->Instance,      //Instance
 FltObjects->FileObject,    //FileObject
           &oldContext);              //OldContext
...
if (oldContext != NULL) {
 FltReleaseContext(oldContext);
}
```

この例では、 [**Fltdeletestreamcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)はストリームからストリームコンテキストを削除しますが、 *Oldcontext*パラメーターが**NULL**ではないため、コンテキストの参照カウントをデクリメントしません。 **Fltdeletestreamcontext**は、 *oldcontext*パラメーターで削除されたコンテキストのアドレスを返します。 必要な処理を実行した後、呼び出し元は**FltReleaseContext**を呼び出すことによって、削除されたコンテキストを解放する必要があります。

 

 




