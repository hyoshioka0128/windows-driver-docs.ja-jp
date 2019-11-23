---
title: ストリーム別コンテキストの削除
description: ストリーム別コンテキストの削除
ms.assetid: 293a2ba2-af8a-4c1b-bc35-5e37e6e84d57
keywords:
- フィルタードライバー WDK ファイルシステム、ストリームごとのコンテキスト追跡
- ファイルシステムフィルタードライバー WDK、ストリームごとのコンテキスト追跡
- ストリームごとのコンテキスト追跡 WDK ファイルシステム
- ストリームごとのコンテキストの追跡 WDK ファイルシステム
- ストリームごとのコンテキストの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d208588b510e872e6b4e4e867b5f00622a369d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841442"
---
# <a name="deleting-a-per-stream-context"></a>ストリーム別コンテキストの削除


## <span id="ddk_deleting_a_per_stream_context_if"></span><span id="DDK_DELETING_A_PER_STREAM_CONTEXT_IF"></span>


ファイルストリームに関連付けられているストリームごとのコンテキストが不要になった場合は、削除する必要があります。 ストリームコンテキストは、次の2つの方法のいずれかで削除されます。

-   手動で、フィルタードライバーが[**Fsrtlremoveperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)を呼び出します。

-   自動的に、ファイルシステムが[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)を呼び出し、その後、ストリームコンテキストの[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチンが呼び出されます。

### <a name="span-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanspan-idwhen_the_filter_deletes_the_per-stream_contextspanwhen-the-filter-deletes-the-per-stream-context"></a><span id="When_the_Filter_Deletes_the_Per-Stream_Context"></span><span id="when_the_filter_deletes_the_per-stream_context"></span><span id="WHEN_THE_FILTER_DELETES_THE_PER-STREAM_CONTEXT"></span>フィルターがストリームごとのコンテキストを削除する場合

ファイルストリームがまだ開いている間に、フィルタードライバーがファイルストリームのストリームごとのコンテキストを削除する必要がある場合、最初に[**Fsrtlremoveperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)を呼び出して、指定されたファイルに関連付けられているコンテキストのグローバルリストからコンテキストを削除します。 **Fsrtlremoveperstreamcontext**を呼び出した後は、通常、このフィルターによってコンテキスト構造が解放されます。

**注**   は、フィルタードライバーが[**Fsrtlinsertperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)を呼び出してストリームごとのコンテキスト構造をファイルストリームに関連付けると、それを解放する前に、そのコンテキストに対して[**fsrtlremoveperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff547238)を呼び出す必要があることに注意してください。 それ以外の場合、ファイルストリームが閉じられると、システムがクラッシュします。

 

### <a name="span-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanspan-idwhen_the_per-stream_context_s_freecallback_is_calledspanwhen-the-per-stream-contexts-freecallback-is-called"></a><span id="When_the_Per-Stream_Context_s_FreeCallback_Is_Called"></span><span id="when_the_per-stream_context_s_freecallback_is_called"></span><span id="WHEN_THE_PER-STREAM_CONTEXT_S_FREECALLBACK_IS_CALLED"></span>ストリームごとのコンテキストの FreeCallback が呼び出されたとき

ファイルストリームを閉じたり削除したりすると、ファイルシステムによってファイルストリームのストリームコンテキストが解放されます。 この時点でも、ファイルシステムは[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)を呼び出し、そのファイルストリームのコンテキストのグローバルリストに含まれるすべてのストリームコンテキストに対して登録されている[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチンを呼び出します。 ( **FreeCallback**ルーチンは、フィルタードライバーが[**Fsrtlinitperstreamcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlinitperstreamcontext)を呼び出してストリームごとのコンテキスト構造を初期化するときに登録されます。 詳細については、「 **FSRTL\_PER\_STREAM\_CONTEXT**」を参照してください)。

**注**   フィルタードライバーが[**Fsrtlinsertperstreamcontext**](https://msdn.microsoft.com/library/windows/hardware/ff546194)を呼び出してストリームごとのコンテキスト構造をファイルストリームに関連付けると、ファイルシステムは、ストリームへの開いている参照がなくなったときに、フィルターのストリームごとのコンテキストの[**FreeCallback**](https://msdn.microsoft.com/library/windows/hardware/ff547357)ルーチンが呼び出されることを保証します。

 

 

 




