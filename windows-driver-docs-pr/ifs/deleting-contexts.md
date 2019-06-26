---
title: コンテキストの削除
description: コンテキストの削除
ms.assetid: 43a30a75-4344-4fc5-ad57-28b48c2e54a8
keywords:
- WDK のコンテキストのファイル システム ミニフィルターを削除します。
- コンテキストを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c56ebde9775c8dcc7dcec160cb4a5b4eb0c576b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376112"
---
# <a name="deleting-contexts"></a>コンテキストの削除


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


正常な呼び出しで設定されているすべてのコンテキスト**FltSet***Xxx***コンテキスト**最終的に削除する必要があります。 ただし、フィルター マネージャーに関連付けられている、オブジェクトが削除されるは、ミニフィルター ドライバーのインスタンスが、ボリュームからデタッチされている場合、またはミニフィルター ドライバーを読み込むときにコンテキストを自動的に削除します。 したがって、ミニフィルター ドライバー コンテキストを明示的に削除するために必要なことはほとんどありませんが。

ミニフィルター ドライバーは呼び出すことにより、コンテキストを削除することができます**FltDelete***Xxx***コンテキスト**ここで、 *Xxx*コンテキスト型、または呼び出すことによって[ **FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)します。

コンテキストは、オブジェクトの現在設定されている場合にのみ削除できます。 これがまだ設定されていない場合、または成功した呼び出しで既に交換している場合、コンテキストを削除できません**FltSet***Xxx***コンテキスト**します。

呼び出しで**FltDelete***Xxx***コンテキスト**で古いコンテキストが返される、 *OldContext*以外である場合は、パラメーター**NULL**します。 場合、 *OldContext*パラメーターが**NULL**、ミニフィルター ドライバーに未解決の参照がない限りは解放すると、コンテキストの参照カウントはフィルター マネージャーをデクリメントします。

次のコード例では、ストリーム コンテキストを削除する方法を示します。

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

この例で[ **FltDeleteStreamContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamcontext)削除のため、ストリームからストリームのコンテキストがコンテキストの参照カウントをデクリメントされません、 *OldContext*パラメーターは非**NULL**します。 **FltDeleteStreamContext**で削除されたコンテキストのアドレスを返して、 *OldContext*パラメーター。 呼び出し元が呼び出すことによって削除されたコンテキストを解放する必要がありますいずれかを実行するには、処理が必要に応じて後、 **FltReleaseContext**します。

 

 




